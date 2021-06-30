---
id: node_monitoring
title: Giám sát Node
---

import useBaseUrl from '@docusaurus/useBaseUrl'; 

Trong chương này chúng tôi sẽ  hướng dẫn thiết lập giám sát local node trình xác thực của bạn.

## Điều Kiện Tiên Quyết {#prerequisites}

[validator node](/node_setup) của bạn phải dang hoạt động.

Hướng dẫn này đã được thử nghiệm trên bản phát hành Ubuntu 20.04 LTS.

## Thiết Lập Prometheus  {#prometheus-setup}

Ở bước đầu tiên, chúng ta sẽ thiết lập Prometheus server.

### Thư Mục và Người Dùng {#user-and-directories}

Chúng ta tạo một người dùng chỉ cho mục đích giám sát, người dùng đó không có thư mục chính và không thể dùng để đăng nhập .


```shell script
$ sudo useradd --no-create-home --shell /usr/sbin/nologin prometheus
```

Sau đó, chúng ta tạo các thư mục cho tệp thực thi và tệp cấu hình.


```shell script
$ sudo mkdir /etc/prometheus
$ sudo mkdir /var/lib/prometheus
```

Thay đổi quyền sở hữu các thư mục để hạn chế chúng với người dùng giám sát mới .

```shell script
$ sudo chown -R prometheus:prometheus /etc/prometheus
$ sudo chown -R prometheus:prometheus /var/lib/prometheus
```

### Cài Đặt Prometheus {#install-prometheus}

Kiểm tra phiên bản mới nhất của Prometheus tại [GitHub release page](https://github.com/prometheus/prometheus/releases/). 
Tại thời điểm viết bài này, phiên bản mới nhất là v2.25.2. Cài phiên bản phát hành mới nhất theo các câu lệnh sau.

```shell script
# download prometheus
$ wget https://github.com/prometheus/prometheus/releases/download/v2.25.2/prometheus-2.25.2.linux-amd64.tar.gz

# unpack the binaries
$ tar xfz prometheus-*.tar.gz

# enter the unpacked directory
$ cd prometheus-2.25.2.linux-amd64
```

Bây giờ sao chép các tệp Binary vào thư mục cục bộ.

```shell script
$ sudo cp ./prometheus /usr/local/bin/
$ sudo cp ./promtool /usr/local/bin/
```

Bây giờ chúng ta cần gán các mã Binary đó cho người dùng mới được tạo .

```shell script
$ sudo chown prometheus:prometheus /usr/local/bin/prometheus
$ sudo chown prometheus:prometheus /usr/local/bin/promtool
```

Tiếp theo, chúng ta sẽ sao chép giao diện web và thiết lập trước cấu hình.

```shell script
$ sudo cp -r ./consoles /etc/prometheus
$ sudo cp -r ./console_libraries /etc/prometheus
```

Có thể bạn đã đoán ra nhưng chúng ta cũng đang thay đổi quyền sở hữu của những thư mục đó.

```shell script
$ sudo chown -R prometheus:prometheus /etc/prometheus/consoles
$ sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
```

Bây giờ chúng ta có mọi thứ chúng ta cần từ gói đã tải xuống, vì vậy chúng ta sẽ quay lại một bước và thực hiện một số thao tác dọn dẹp.

```shell script
$ cd .. && rm -rf prometheus*
```

Hãy tạo tệp cấu hình `YAML` cho Prometheus bằng trình chỉnh sửa mà bạn chọn (nano / vim / pico).


```shell script
$ sudo nano /etc/prometheus/prometheus.yml
```

Cấu hình của chúng ta được chia thành ba phần:

* `global`:  Đặt các giá trị mặc định cho `scrape_interval` và khoảng thời gian thực thi quy tắc với `eval_interval`
* `rule_files`:  Xác định rõ các tệp quy tắc mà máy chủ Prometheus sẽ tải
* `scrape_configs`:  đây là nơi bạn đặt tài nguyên giám sát

Chúng ta sẽ giữ nó cơ bản nhất và kết thúc với một cái gì đó như thế này:

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

Công việc thu thập dữ liệu đầu tiên là xuất dữ liệu của chính Prometheus, công việc thứ hai xuất các chỉ số của HydraDX node.
Chúng tôi đã điều chỉnh `scrape_interval` của cả hai việc để có được số liệu thống kê chi tiết hơn. Điều này quan trọng hơn các giá trị chung.
`target` trong `static_configs` cài đặt nơi trình xuất chạy, chúng tôi bám vào các cổng mặc định ở đây.

Sau khi lưu cấu hình, chúng tôi sẽ  thay đổi quyền sở hữu một lần nữa.

```shell script
$ sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml
```

### Bắt đầu chạy Prometheus {#starting-prometheus}

Để có hệ thống giám sát mạng Prometheus tự động chạy trên nền chúng ta sẽ sử dụng  `systemd`.
Tạo một cấu hình mới (với trình chỉnh sửa mà bạn chọn ):

````shell script
$ sudo nano /etc/systemd/system/prometheus.service
````

Dán cấu hình bên dưới và lưu tệp đó. 

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

Tiếp theo chúng ta sẽ thực hiện ba bước sau:

`systemctl deamon-reload`  tải các cấu hình mới và cập nhật hiện có
`systemctl enable`  kích hoạt dịch vụ mới của chúng tôi
`systemctl start`  kích hoạt việc thực thi dịch vụ

 
Bạn có thể thực hiện các bước ở trên bằng một lệnh bằng câu lệnh bên dưới:

```shell script
$ sudo systemctl daemon-reload && systemctl enable prometheus && systemctl start prometheus
```

Bây giờ bạn có thể truy cập giao diện web của hệ thống giám sát mạng Prometheus tại http://localhost:9090/.

## Node Exporter {#node-exporter}

Chúng tôi sẽ cài đặt Node Exporter để loại bỏ các chỉ số máy chủ sẽ được sử dụng trong trang tổng quan.
Vui lòng kiểm tra phiên bản phát hành mới nhất  [ở đây](https://github.com/prometheus/node_exporter/releases/) và cập nhật câu lệnh.  
Tại thời điểm viết phiên bản mới nhất là `1.1.2`.

### Cài Đặt Node Exporter {#install-node-exporter}

Tải xuống bản phát hành mới nhất.

```shell script
$ wget https://github.com/prometheus/node_exporter/releases/download/v1.1.2/node_exporter-1.1.2.linux-amd64.tar.gz
```

 Giải nén tệp bạn vừa tải xuống. Nó sẽ tạo một thư mục gọi là  `node_exporter-1.1.2.linux-amd64`.

```shell script
$ tar xvf node_exporter-1.1.2.linux-amd64.tar.gz
```

Tiếp theo chúng ta copy những tệp đó vào trong thư mục ứng dụng local và chỉ định nó cho người dùng giám sát của chúng ta.

```shell script
# copy binary
$ cp node_exporter-1.1.2.linux-amd64/node_exporter /usr/local/bin

# set ownership
$ sudo chown prometheus:prometheus /usr/local/bin/node_exporter
```

Chúng ta có thể thực hiện một số dọn dẹp và xóa những gói đã tải xuống và giải nén ngay bây giờ.

```shell script
$ rm -rf node_exporter*
```

### Tạo một Systemd Service {#create-a-systemd-service}

Tương tự như chương trình giám sát prometheus, chúng ta cũng muốn Node Exporter chạy như một dịch vụ.
Tạo một systemd service với trình chỉnh sửa mà bạn chọn.

```shell script
$ sudo nano /etc/systemd/system/node_exporter.service
```

Và dán cấu hình sau vào đó.

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

Bây giờ chúng ta sẽ kích hoạt và bắt đầu dịch vụ với một dòng lệnh:

```shell script
$ sudo systemctl daemon-reload && systemctl enable node_exporter && systemctl start node_exporter
```

### Thêm công việc trích xuất dữ liệu cho Node Exporter {#add-scrape-job-for-node-exporter}

Node Exporter hiện đã được thiết lập và đang chạy nhưng chúng ta cần yêu cầu hệ thống giám sát Prometheus trích xuất dữ liệu của nó.
Chúng ta sẽ mở lại tệp cấu hình với trình chỉnh sửa đã chọn.

```shell script
$ sudo nano /etc/prometheus/prometheus.yml
```

Ở cuối của tệp, chúng ta sẽ thêm một cấu hình trình xuất dữ liệu nữa
Dán nội dung sau và lưu tệp.

```yaml
  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']
```

Việc thay đổi các cấu hình, quá trình khởi động lại dịch vụ hệ thống giám sát Prometheus là bắt buộc.

```shell script
$ sudo systemctl restart prometheus.service 
```

Các chỉ số máy chủ của bạn hiện đã được trính xuát dữ liệu và có thể được tìm thấy trong giao diện web hệ thống giám sát Prometheus.
Chúng ta sẽ cần chúng sau này cho bảng điều khiển của chúng ta. 

## Xây dựng Grafana  {#grafana-setup}

Chúng ta có thể thấy các chỉ số của mình trong giao diện web, nhưng đó không phải là cách chúng ta muốn theo dõi.
Chúng tôi muốn nó đẹp . Đó là nơi Grafana phát huy tác dụng.

### Cài đặt Grafana {#install-grafana}

Vui lòng kiểm tra phiên bản Grafana mới nhất là gì [Với link này](https://grafana.com/grafana/download?platform=linux).  
Bạn có thể thay đổi số phiên bản trong các lệnh sau hoặc sao chép lệnh cài đặt trực tiếp từ liên kết.
Tại thời điểm viết phiên bản mới nhất là `7.5.1`.

```shell script
$ sudo apt-get install -y adduser libfontconfig1
$ wget https://dl.grafana.com/oss/release/grafana_7.5.1_amd64.deb
$ sudo dpkg -i grafana_7.5.1_amd64.deb
```

Gói cài đặt này đi kèm với `systemd` -dịch vụ mà chúng ta sẽ cấu hình và khởi động giống như dịch vụ hệ thống giám sát Prometheus.

```shell script
$ sudo systemctl daemon-reload && sudo systemctl enable grafana-server && sudo systemctl start grafana-server
```

### Truy cập giao diện web {#accessing-the-web-interface}

Chúng ta có thể mở giao diện web Grafana tại  http://localhost:3000/.  
Tài khoản đăng nhập mặc định của Grafana là:  
tài khoản: `admin`  
Mật khẩu: `admin`  

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-home.png')} />
</div>

### Cấu hình nguồn dữ liệu {#configuring-the-datasource}

Vui lòng nhấp vào setting với logo hình bánh răng trong menu và chọn "datasources".
Trong cửa sổ tiếp theo bạn nhấn vào "Add Datasource" và chọn "Prometheus".
Trong biểu mẫu sau, bạn không cần thay đổi bất cứ điều gì ngoài URL.

Đặt URL là `http://localhost:9090/` và nhấn vào `Save and Test`.  

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-datasource.png')} />
</div>

### Nhập vào Dashboard {#importing-the-dashboard}

Vui lòng nhấp vào `Plus` -nút trong điều hướng chính và chọn `import`

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-import.png')} />
</div>  

We will use the Chúng ta sẽ sử dụng  [HydraDX Dashboard](https://grafana.com/grafana/dashboards/14158)  và để tải nó, bạn đơn giản chỉ cần đặt ID là `14158` và nhấn vào nút `Load`  

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-import-options.png')} />
</div>  

Bạn không cần cấu hình nhiều ở đây, chỉ cần đảm bảo Hệ thống giám sát `Prometheus` được sử dụng làm datasource`datasource`.
Bây giờ bạn có thể hoàn tất quá trình nhập.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/node-monitoring/grafana-dashboard.png')} />
</div>  

Bây giờ bạn sẽ thấy trang tổng quan của mình ngay lập tức.
Nếu một số bảng trống, vui lòng đảm bảo lựa chọn của bạn phía trên các bảng như sau:
* `Chain Metrics`: Substrate  
* `Chain Instance`: localhost:9615  
* `Server Job`: node_exporter  
* `Server Host`: localhost:9100  
