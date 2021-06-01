---
id: node_setup
title: Thiết lập một Node Trình Xác Thực
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Phần này sẽ hướng dẫn bạn quá trình thiết lập và chạy một HydraDX node.

:::warning

Việc chạy Node Trình Xác Thực thực yêu cầu một bộ kỹ năng kỹ thuật nhất định cần thiết để thiết lập node phù hợp và để đảm bảo thời gian hoạt động của nó. Nếu bạn không chắc mình đang làm gì ở đây, chúng tôi khuyên bạn nên [đề cử HDX của bạn](/start_nominating) cho một validator có kinh nghiệm. Bằng cách làm như vậy, bạn bảo vệ bản thân và những người đề cử của bạn trước sự mất mát của quỹ một cách không chủ ý.

:::

## 00 Thông số kỹ thuật yêu cầu {#00-required-technical-specifications}

Các thông số kỹ thuật sau đây là yêu cầu tối thiểu để chạy một Node trình xác thực HydraDX :

* Hệ điều hành OS: Ubuntu 20.04
* CPU: Intel Core i7-7700K @ 4.5Ghz (hoặc hiệu suất lõi đơn tương đương)
* Bộ nhớ: 64GB RAM
* Ổ cứng : NVMe SSD dung lượng ít nhất 200GB (data footprint sẽ tăng theo thời gian)

:::note

Đây là những yêu cầu kỹ thuật tối thiểu đã được xác minh bởi team. Đảm bảo rằng máy của bạn có đủ tài nguyên để chạy một node? Chạy [Hiệu suất Benchmark](/performance_benchmark) để xác minh điều đó.

:::


## 01 Kiểm tra đồng bộ đồng hồ hệ thống của bạn {#01-check-whether-your-system-clock-is-synchronized}

Trước khi chạy một node, bạn nên đảm bảo rằng đồng hồ hệ thống của bạn được đồng bộ - điều này rất quan trọng vì các trình xác thực hoạt động cùng nhau. Trên Ubuntu 20.04, đồng hồ hệ thống phải được đồng bộ theo mặc định. Để xác minh, hãy chạy lệnh sau và kiểm tra đầu ra:

```bash
$ timedatectl | grep "System clock"
System clock synchronized: yes
```

Nếu đầu ra khác, thì bạn có thể cài đặt NTP theo cách thủ công và xác minh lại rằng đồng hồ hệ thống của bạn đã được đồng bộ:

```bash
$ apt install ntp
$ ntpq -p
```

## 02Điều chỉnh cài đặt tường lửa của bạn{#02-adjust-your-firewall-settings}

Cổng `30333` được sử dụng cho các kết nối ngang hàng với các node khác. Nếu bạn đang chạy node với tư cách là một trình xác thực, chúng tôi khuyên bạn nên thiết lập tường lửa và định cấu hình để chỉ hiển thị cổng này cho các kết nối từ xa.
Nếu bạn * không * chạy node với tư cách là một trình xác thực, bạn cũng có thể xem xét việc hiển thị `9944`(đối với các kết nối websocket RPC với các ứng dụng bên ngoài) và `9933` (đối với các yêu cầu HTTP tới node của bạn). Bạn có thể sử dụng cổng `9944` để kết nối với nodecủa mình bằng [Polkadot/apps](/polkadotjs_apps_local).

## 03 Tải xuống hoặc xây dựng bản Binary {#03-download-or-build-a-binary}

Bạn có thể tải xuống Binary của bản phát hành mới nhất của chúng tôi trên [github](https://github.com/galacticcouncil/HydraDX-node/releases).
Ngoài ra, bạn có xây dựng Binary từ nguồn:

```bash
# Install dependencies
$ curl https://getsubstrate.io -sSf | bash -s -- --fast

# Fetch source of the latest stable release
$ git clone https://github.com/galacticcouncil/HydraDX-node -b stable

# Build the binary
$ cd HydraDX-node/
$ cargo build --release
```

Nếu bạn đã xây dựng Binary theo các bước ở trên, thì đường dẫn đến Binary của bạn là:

```
target/release/hydra-dx
```

## 04 Chạy bản Binary {#04-run-the-binary}

Bạn có thể chạy bản Binary bằng cách thực hiện lệnh sau:

```bash
$ {PATH_TO_YOUR_BINARY} --chain lerna --name {YOUR_NODE_NAME} --validator
```

:::note

Node trình xác thực yêu cầu toàn bộ cơ sở dữ liệu chuỗi. Nếu bạn đã chạy node trước đó mà không có  `--validator` flag, bạn sẽ cần phải đồng bộ hóa lại cơ sở dữ liệu bằng cách xóa chuỗi trước khi khởi chạy node.
```bash
$ {PATH_TO_YOUR_BINARY} purge-chain --chain lerna
```

:::

Bên cạnh đường dẫn đến Binary của bạn (xem ở trên), bạn cần chỉ định tên node, nó sẽ được sử dụng để xác định node của bạn trong [Telemetry](https://telemetry.hydradx.io/#/HydraDX%20Snakenet%20Gen2)  ở đó bạn có thể tìm thấy danh sách tất cả các node đang chạy trên HydraDX Snakenet.

## 05 Chạy với Systemd {#05-running-with-systemd}

Để đảm bảo rằng node của bạn được tự động khởi động khi máy của bạn khởi động lại, chúng tôi khuyên bạn nên chạy  HydraDX node như một quy trình systemd. Để làm như vậy, hãy tạo tệp sau và chèn nội dung trong khi thay thế các biến được chỉ định là `{VARIABLE} ':

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

Thiết lập RestartSec được khuyến khích vì nó sẽ trì hoãn việc khởi động lại node trong trường hợp có sự cố. Điều này cho phép mọi dữ liệu chưa được lưu trữ (chẳng hạn như phiếu đồng thuận) được ghi vào ổ cứng trước khi node được khởi động lại. Khởi động lại node ngay lập tức sau khi nó gặp sự cố có thể gây ra sự cố định vị trí hoặc ký hai lần, cuối cùng dẫn đến việc bị slashing.

:::

Sau khi tạo tệp cấu hình, bạn có thể tương tác với node trình xác thực HydraDX  của mình như một quy trình hệ thống:

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

Node HydraDX  của bạn hiện đã được định cấu hình và đang chạy!
Bây giờ bạn có thể hoàn thành các bước cuối cùng để [Bắt đầu trình xác thực](/start_validating).
