| id                 | tytuł              |
| ------------------ | ------------------ |
| node_monitoring_pl | Monitorowanie Node |

import useBaseUrl from '@docusaurus/useBaseUrl'; 

W tej części dowiemy się jak ustawić lokalny monitoring Twojego node

## Warunki wstępne

Musisz mieć działającego node.
Instrukcja została przetestowania na systemie operacyjnym Ubuntu 20.04 LTS

## Ustawienia Prometheus

W pierwszej kolejności skonfigurujemy serwer Prometheus

### Użytkownik i katalogi

Tworzymy nowego użytkownika w celu monitorowania, lecz na razie nie posiada on katalogu domowego i 
nie może się zalogować.


```shell script
$ sudo useradd --no-create-home --shell /usr/sbin/nologin prometheus
```

Dalej tworzymy katalogi aby być w stanie konfigurować i uruchamiać system

```shell script
$ sudo mkdir /etc/prometheus
$ sudo mkdir /var/lib/prometheus
```

Zmień uprawnienia wyżej wymienionych katalogów aby ograniczyć je do nowo stworzonego użytkownika

```shell script
$ sudo chown -R prometheus:prometheus /etc/prometheus
$ sudo chown -R prometheus:prometheus /var/lib/prometheus
```

### Instalacja Prometheus

Sprawdź ostatnią aktualną wersje Prometheus w [GitHub release page](https://github.com/prometheus/prometheus/releases/).
W czasie pisania tego artykułu jest to v2.52.2. Wstaw ostatnią wersje w poniższej komendzie.

```shell script
# download prometheus
$ wget https://github.com/prometheus/prometheus/releases/download/v2.25.2/prometheus-2.25.2.linux-amd64.tar.gz

# unpack the binaries
$ tar xfz prometheus-*.tar.gz

# enter the unpacked directory
$ cd prometheus-2.25.2.linux-amd64
```

Nastepnie skopiuj binarki do lokalnych folderów

```shell script
$ sudo cp ./prometheus /usr/local/bin/
$ sudo cp ./promtool /usr/local/bin/
```

Musimy dostosować te binarki do naszego świeżo utworzonego użytkownika

```shell script
$ sudo chown prometheus:prometheus /usr/local/bin/prometheus
$ sudo chown prometheus:prometheus /usr/local/bin/promtool
```

W dalszej kolejności skopiujemy interfejs webowy i predefiniowane konfiguracje

```shell script
$ sudo cp -r ./consoles /etc/prometheus
$ sudo cp -r ./console_libraries /etc/prometheus
```

Jak zapewne się domyślasz musimy również zmienić uprawnienia dla tych katalogów

```shell script
$ sudo chown -R prometheus:prometheus /etc/prometheus/consoles
$ sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
```

Mamy wszystko czego potrzebujemy więc cofamy się katalog niżej i czyścimy prometheus

```shell script
$ cd .. && rm -rf prometheus*
```

Tworzymy teraz plik konfiguracyjny 'YAML' dla Prometheus za pomocą edytora (nano / vim / pico)

```shell script
$ sudo nano /etc/prometheus/prometheus.yml
```

Nasza konfiguracja podzielona jest na 3 części:

* `global`: ustawia globalne wartości dla `scrape_interval` zasady uruchamiania pliku konfiguracyjnego `evaluation_interval`
* `rule_files`: definiuje w jaki sposób pliki powinny być wczytane przez server Prometheus
* `scrape_configs`: definiujemy zasoby minitoringu

Poniższy przykład przedstawia podstawową konfiguracje:

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  # - "weHaveNo.rules"

scrape_configs:
  - job_name: "prometheus"
    scrape_interval: 5s
    static_configs:
      - targets: ["localhost:9090"]
  - job_name: "substrate_node"
    scrape_interval: 5s
    static_configs:
      - targets: ["localhost:9615"]
```

Pierwsze scrape job przedstawia ustawienia dla Prometheusa, z kolei drugi eksportuje je dla walidatora HydraDX.
Dostosowujemy `scrape_interval` dla obu jobów aby dostać szczegółowe statystyki. Nadpisują one ustawienia globalne.
Plik `target` w `static_configs` ustawia gdzie exporters są uruchomione, zostawiamy porty domyślne.

Po zapisaniu konfiguracji ustawiamy znowu uprawienia pliku dla użytkownika

```shell script
$ sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml
```

### Rozpoczęcie pracy Prometheus

Aby Prometheus uruchamiał się automatycznie musimy skonfiguracja w tle 'systemd'.
W tym celu stwórz nową konfiguracje (użyj edytora jakiego chcesz):

````shell script
$ sudo nano /etc/systemd/system/prometheus.service
````

Wklej poniższą konfiguracje i zapisz plik:

```
[Unit]
  Description=Prometheus Monitoring
  Wants=network-online.target
  After=network-online.target

[Service]
  User=prometheus
  Group=prometheus
  Type=simple
  ExecStart=/usr/local/bin/prometheus \
  --config.file /etc/prometheus/prometheus.yml \
  --storage.tsdb.path /var/lib/prometheus/ \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries
  ExecReload=/bin/kill -HUP $MAINPID

[Install]
  WantedBy=multi-user.target
```

Następnie wykonaj trzy poniższe polecenia:
`systemctl deamon-reload` wczytuje konfiguracje i zaktualizuje istniejącą
`systemctl enable` aktywuje nowy serwis
`systemctl start` uruchomia aktywowany serwis

Możesz wykonać powyższe trzy kroki w jednym poleceniu:

```shell script
$ sudo systemctl daemon-reload && systemctl enable prometheus && systemctl start prometheus
```

Powinieneś mieć dostęp do interfejsu webowego Prometheus przez link http://localhost:9090/.

## Node Exporter

Zainstalujemy Node Exporter do pobierania statystyk z serwera, które będą widoczne na stronie. Upewnij się, że używasz aktualną wersje node exporter [here](https://github.com/prometheus/node_exporter/releases/).
W trakcie pisania artykułu była to wersja `1.1'2`.

### Instalacja Node Exporter

Pobierz ostatnią wersje

```shell script
$ wget https://github.com/prometheus/node_exporter/releases/download/v1.1.2/node_exporter-1.1.2.linux-amd64.tar.gz
```

Rozpakuj pobrany plik. Powinien zostać utworzony folder o nazwie `node_exporter-1.1.2.linux-amd64`

```shell script
$ tar xvf node_exporter-1.1.2.linux-amd64.tar.gz
```

Następnie kopiujemy binarke do naszego lokalnego katalogu i nadajemy uprawnienia dla naszego użytkownika.

```shell script
# copy binary
$ cp node_exporter-1.1.2.linux-amd64/node_exporter /usr/local/bin

# set ownership
$ sudo chown prometheus:prometheus /usr/local/bin/node_exporter
```

Czyścimy i usuwamy pograną oraz nierozpakowaną paczkę.

```shell script
$ rm -rf node_exporter*
```

### Tworzymy Systemd Serwis

Podobnie jak w przypadku Prometheus chcemy uruchomić serwis systemd dla Node Exporter.

```shell script
$ sudo nano /etc/systemd/system/node_exporter.service
```

Wklej poniższą konfiguracje

```
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

Aktywuj i uruchom serwis z pomocą poniższej komendy.

```shell script
$ sudo systemctl daemon-reload && systemctl enable node_exporter && systemctl start node_exporter
```

### Dodaj Scrape Job dla Node Exporter

Node Exporter jest uruchomiony ale musimy jeszcze powiedzieć Prometheus aby pobiera dane. Otwórz znowu plik konfiguracyjny.

```shell script
$ sudo nano /etc/prometheus/prometheus.yml
```

Na końcu pliku dodaj poniższą konfiguracje.

```yaml
  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']
```

Zapisz ustawienia i uruchom Prometheus systemd jeszcze raz (wymagane).

```shell script
$ sudo systemctl restart prometheus.service 
```

Od teraz Twój serwer do statystyk pobiera dane i jest dostepny w postaci interfejsu webowego. Będziemy go później potrzebować.

## Konfiguracja Grafana

Możemy podejrzeć nasze metryki na stronie ale do pełni szczęścia potrzebujemy ładnego i przejrzystego interfejsu. W tym celu użyjemy Grafana.

### Instalacja Grafana

Sprawdź ostatnią wersje Grafana [with this link](https://grafana.com/grafana/download?platform=linux).
Możesz albo zmienić wersje z poniższą komendą lub skopiować komende bezprośrednio z linku. W momencie pisania artykułu była to wersja `7.5.1`.

```shell script
$ sudo apt-get install -y adduser libfontconfig1
$ wget https://dl.grafana.com/oss/release/grafana_7.5.1_amd64.deb
$ sudo dpkg -i grafana_7.5.1_amd64.deb
```

Paczka jest dostosowana do `systemd` serwisu, więc od razu możemy go uruchomić z poniższą komendą, analogicznie jak w przypadku Prometheus.

```shell script
$ sudo systemctl daemon-reload && sudo systemctl enable grafana-server && sudo systemctl start grafana-server
```

### Dostęp do interfejsu webowego

Jesteśmy w stanie uruchomić interfejs webowy Grafana pod adresem http://localhost:3000/.
Domyślne login i hasło:  
User: `admin`  
Password: `admin`  

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-home.png')} />
</div>

### Konfiguracja Datasource

Kliknij w menu ikone koła zębatego (ustawienia) i wybierz datasources.
W kolejnym okienku kliknij "Add Datasource" i wybierz "Prometheus". 

W poniższym formularzu jedyne co musisz zmieniać to adres URL.
Ustaw `http://localhost:9090/` i kliknij `Save and Test`.  

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-datasource.png')} />
</div>

### Importowanie Dashboard

Kliknij przycisk `Plus` w glównym menu nawigacji i kliknij `import`.  

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-import.png')} />
</div>  

Będziemy używać [HydraDX Dashboard](https://grafana.com/grafana/dashboards/14158)
i wczytywać to do prostego wejścia id `14158` i uderzać przycisk `Load`

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-import-options.png')} />
</div>  

Nie trzeba tutaj za wiele konfigurowac, po prostu się upewnij, że Prometheus jest używany jako datasource. Możesz zakończy import.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-dashboard.png')} />
</div>  

Powienień teraz widzieć swój dashboard. Jeśli któreś z paneli są puste, upewnij się, że wybór ich jest zgodny z poniższym.    
* `Chain Metrics`: Substrate  
* `Chain Instance`: localhost:9615  
* `Server Job`: node_exporter  
* `Server Host`: localhost:9100 