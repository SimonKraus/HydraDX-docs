---
id: build_dev_chain
title: Thiết lập một Development Chain
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Phần này sẽ hướng dẫn bạn quá trình thiết lập một phiên bản local HydraDX-chain instance để phát triển.

:::note
Bạn đang tìm cách thiết lập một Node cho mục đích trình xác thực? Vui lòng chuyển đến [Hướng dẫn thiết lập trình xác thực ](/node_setup) của chúng tôi.
:::

## 01 Cài đặt các phần phụ thuộc {#01-install-dependencies}

Để chuẩn bị một phiên bản local HydraDX-chain instance để phát triển, máy của bạn cần bao gồm tất cả các phần phụ thuộc để chạy một Substrate chain. Bạn sẽ cần cài đặt môi trường Rust dành cho nhà phát triển và đảm bảo rằng nó được định cấu hình đúng cách để biên dịch "Substrate runtime code" thành mục tiêu WebAssembly (Wasm).

Bạn có thể cài đặt và định cấu hình tất cả các phần phụ thuộc theo cách thủ công sau [Hướng dẫn Substrate ](https://substrate.dev/docs/en/knowledgebase/getting-started), hoặc bạn có thể để câu lệnh này thực hiện tất cả công việc cho bạn:

```bash
$ curl https://getsubstrate.io -sSf | bash -s -- --fast
$ source ~/.cargo/env
```

## 02 Build {#02-build}

Xây dựng môi trường thực thi ban đầu và Wasm :

```bash
# Fetch source of the latest stable release
$ git clone https://github.com/galacticcouncil/HydraDX-node -b stable

# Build the binary
$ cd HydraDX-node/
$ cargo build --release
```

Bạn có thể tìm thấy bản Build ở đây: `./target/release/hydra-dx`.

## 03  Chạy bản Build{#03-run}

Trước khi chạy bản Build của mình, bạn có thể xóa mọi chuỗi phát triển hiện có trên máy của mình (bạn sẽ cần làm điều này thường xuyên trong quá trình phát triển):

```bash
$ ./target/release/hydra-dx purge-chain --dev
```

Chạy bản Build của bạn bằng một trong các lệnh sau:

```bash
$ ./target/release/hydra-dx --dev

# Run with detailed logging
$ RUST_LOG=debug RUST_BACKTRACE=1 ./target/release/hydra-dx -lruntime=debug --dev
```

## 04 Kết nối tới local chain instance {#04-connect-to-your-local-chain-instance}

Bạn có thể kết nối tới HydraDX Dev-Node của bạn bằng Polkadot/apps và thay đổi mạng thành `Development`. Bạn cũng có thể sử dụng link sau
https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/explorer

<img alt="connect to node" src={useBaseUrl('/building/connect-to-node.jpg')} />
