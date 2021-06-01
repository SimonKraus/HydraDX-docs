---
id: performance_benchmark
title: Hiệu Suất Benchmark
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Bạn có thể đảm bảo rằng máy của bạn đáp ứng  [Thông số kỹ thuật yêu cầu](/node_setup#00-required-technical-specifications) bằng cách chạy Hiệu suất Benchmark. Để làm như vậy, hãy làm theo các bước dưới đây:


```bash
# Fetch source of the latest stable release
$ git clone https://github.com/galacticcouncil/HydraDX-node -b stable
$ cd HydraDX-node/

# Prepare for running the benchmark
## Install Rust following https://rustup.rs
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

## Configure Rust
$ ./scripts/init.sh
$ rustup default nightly

## Install additional libraries
$ apt install python3-pip
$ apt install clang

# Run the benchmark
$ ./scripts/check_performance.sh
```

Sau khi thực thi Benchmark, bạn sẽ thấy một kết quả tương tự như sau:

```
         Pallet          |   Time comparison (µs)    |  diff* (µs)   |   diff* (%)    |            |   Rerun
amm                      |     773.00 vs 680.00      |      93.00    |      12.03     |     OK     |
exchange                 |     804.00 vs 720.00      |      84.00    |      10.44     |     OK     |
transaction_multi_payment|     218.00 vs 198.00      |      20.00    |       9.17     |     OK     |

Notes:
- in the diff fields you can see the difference between the reference benchmark time and the benchmark time of your machine
- if diff is positive for all three pallets, your machine covers the minimum requirements for running a HydraDX node
- if diff deviates by -10% or more for some of the pallets, your machine might not be suitable to run a node
```

Bạn có thể thấy sự khác biệt về hiệu suất giữa máy của bạn và thiết lập bắt buộc tối thiểu trong cột **diff* (%)**. Nếu cả ba giá trị trong cột này đều dương, máy của bạn phù hợp để chạy HydraDX validator node. Nếu bất kỳ giá trị nào dưới *-10 %*, chúng tôi không khuyên bạn nên chạy một HydraDX node.

Tham gia Discord với chúng tôi nếu bạn muốn thảo luận về kết quả benchmark của mình, cộng đồng của chúng tôi luôn sẵn lòng trợ giúp.