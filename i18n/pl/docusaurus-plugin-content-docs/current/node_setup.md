---
id: node_setup
title: Set up a HydraDX node
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Ta sekcja przeprowadzi Cię przez proces konfigurowania i uruchamiania noda HydraDX.

:::warning

Uruchomienie noda walidatora wymaga pewnych umiejętności technicznych potrzebnych do prawidłowej konfiguracji noda i zagwarantowania jego ciągłej pracy.  Jeśli nie jesteś pewien, czy dasz sobie radę, zalecamy zamiast tego [stakowanie swoich tokenów HDX](/start_nominating) u doświadczonego walidatora. W ten sposób chronisz siebie i nominatorów przed przypadkową utratą środków.

:::

## 00 Wymagane specyfikacje techniczne {#00-required-technical-specifications}

Do uruchomienia noda walidatora HydraDX wymagane są co najmniej następujące specyfikacje techniczne: 

* OS: Ubuntu 20.04
* Procesor: Intel Core i7-7700K @ 4.5Ghz (albo inny o podobnej wydajności jednego rdzenia)
* Pamięć RAM: 64GB RAM
* Przestrzeń dyskowa: NVMe SSD om pojemności co najmniej 200GB (ilość danych będzie rosła z czasem)

:::note

Są to minimalne wymagania techniczne, które zostały zweryfikowane przez zespół. Chcesz się upewnić, że Twój komputer ma wystarczające zasoby do uruchomienia węzła? Aby się przekonać, przeprowadź [testy wydajnościowe](/performance_benchmark)

:::


## Sprawdź, czy zegar systemowy jest zsynchronizowany {#01-check-whether-your-system-clock-is-synchronized}

Przed uruchomieniem noda należy upewnić się, że zegar systemowy jest zsynchronizowany - jest to ważne, ponieważ walidatorzy współpracują ze sobą. W systemie Ubuntu 20.04 zegar systemowy powinien być domyślnie synchronizowany. Aby sprawdzić, uruchom następujące polecenie i sprawdź dane wyjściowe:

```bash
$ timedatectl | grep "System clock"
System clock synchronized: yes
```

Jeśli wynik jest inny, możesz zainstalować NTP ręcznie i ponownie sprawdzić, czy zegar systemowy jest zsynchronizowany:

```bash
$ apt install ntp
$ ntpq -p
```

## 02 Dostosuj ustawienia zapory sieciowej {#02-adjust-your-firewall-settings}
Port `30333` jest używany do połączeń peer-to-peer z innymi nodami. Jeśli używasz noda jako walidator, zalecamy skonfigurowanie zapory i skonfigurowanie tak, aby udostępniać tylko ten port dla połączeń zdalnych.

Jeśli *nie* używasz noda jako walidator, możesz również rozważyć udostępnienie portu `9944` dla połączeń RPC websocket z zewnętrznymi aplikacjami) i portu `9933` (dla żądań HTTP do Twojego noda). Możesz użyć portu `9944` aby połączyć się ze swoim nodem za pomocą [Polkadot/apps](/polkadotjs_apps_local).

## 03 Pobierz lub utwórz plik binarny {#03-download-or-build-a-binary}
Możesz pobrać plik binarny naszego najnowszego wydania na [github](https://github.com/galacticcouncil/HydraDX-node/releases).

Alternatywnie możesz zbudować plik binarny ze źródła:

```bash
# Install dependencies
$ curl https://getsubstrate.io -sSf | bash -s -- --fast

# Fetch source of the latest stable release
$ git clone https://github.com/galacticcouncil/HydraDX-node -b stable

# Build the binary
$ cd HydraDX-node/
$ cargo build --release
```

Jeśli utworzyłeś plik binarny postępując zgodnie z powyższymi krokami, ścieżka do pliku binarnego jest następująca:
```
target/release/hydra-dx
```

## 04 Uruchom plik {#04-run-the-binary}
Możesz uruchomić plik binarny, wykonując następujące polecenie:

```bash
$ {PATH_TO_YOUR_BINARY} --chain lerna --name {YOUR_NODE_NAME} --validator
```

:::note

Nody walidatorów wymagają całej bazy danych łańcucha. Jeśli wcześniej uruchomiłeś węzeł bez flagi `--validator` będziesz musiał ponownie zsynchronizować bazę danych przez wyczyszczenie łańcucha przed uruchomieniem noda.

```bash
$ {PATH_TO_YOUR_BINARY} purge-chain --chain lerna
```

:::

Oprócz ścieżki do pliku binarnego (patrz powyżej), musisz określić nazwę noda, która będzie używana do identyfikowania twojego noda w [Telemetrii](https://telemetry.polkadot.io/#list/HydraDX%20Snakenet), gdzie możesz znaleźć listę wszystkich nodów działających w HydraDX Snakenet

## 05 Uruchamianie z systemd {#05-running-with-systemd}
Aby upewnić się, że node jest automatycznie uruchamiany po ponownym uruchomieniu komputera, zalecamy uruchomienie noda HydraDX jako procesu systemowego. Aby to zrobić, utwórz następujący plik i wstaw zawartość, zastępując zmienne wskazane jako `{VARIABLE}`:

```bash
$ touch /etc/systemd/system/hydradx-validator.service
```

```
[Unit]
Description=HydraDX validator

[Service]
Type=exec
User={UNIX_USER}
ExecStart={PATH_TO_YOUR_BINARY} --chain lerna --name {YOUR_NODE_NAME} --validator
Restart=always
RestartSec=120

[Install]
WantedBy=multi-user.target
```

:::note
Ustawienie RestartSec jest zalecane, ponieważ opóźnia restart węzła w przypadku awarii. Pozwala to na zapisanie wszelkich nieutrwalonych danych (takich jak głosy konsensusu) na dysku przed ponownym uruchomieniem noda. Ponowne uruchomienie noda natychmiast po awarii może spowodować niejednoznaczność lub podwójne podpisywanie, ostatecznie skutkujące karą (slash).
:::

Po utworzeniu pliku konfiguracyjnego możesz używać nod HydraDX jako procesu systemowego:

```bash
# Start the node at system boot
$ systemctl enable hydradx-validator.service

# Start the node manually
$ systemctl start hydradx-validator.service

# Check the status of the node
$ systemctl status hydradx-validator.service

# Check the logs of the node
$ journalctl -f -u hydradx-validator.service
```

Twój węzeł HydraDX jest teraz skonfigurowany i działa!

Możesz teraz wykonać ostatnie kroki, aby [rozpocząć walidację](/start_validating).
