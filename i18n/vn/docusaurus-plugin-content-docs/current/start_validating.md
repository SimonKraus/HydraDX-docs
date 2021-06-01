---
id: start_validating 
title: Trở thành một trình xác thực
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Sau khi [Thiêt lấp HydraDX node của bạn](/node_setup), bạn cần góp cổ phần token HDX và cài đặt key cho trình xác thực trước khi có thể bắt đầu xác thực.


:::warning

Việc chạy một node trình xác thực yêu cầu một bộ kỹ năng kỹ thuật nhất định cần thiết để thiết lập node phù hợp và để đảm bảo thời gian hoạt động của nó. Chúng tôi cũng yêu cầu trình xác thực luôn chạy node bằng bản phát hành ổn định mới nhất. Nếu bạn không chắc mình đang làm gì ở đây, chúng tôi khuyên bạn nên [đề cử HDX của mình](/start_nominating) cho một trình xác thực có kinh nghiệm. Bằng cách làm như vậy, bạn bảo vệ bản thân và những người được đề cử của bạn trước sự vô ý làm mất mát của quỹ.

:::

## 01 Góp cổ phần HDX token {#01-bond-hdx-tokens}


Để tham gia vào mạng với tư cách là một node trình xác thực, bạn cần phải góp cổ phần một số lượng token HDX. Nếu bạn không có bất kỳ HDX nào, bạn không thể tham gia vào giai đoạn đầu của testnet. Tuy nhiên, một số tin tức thú vị sẽ được nhóm công bố trong những tuần tới vì vậy hãy tiếp tục ở lại bài này và đăng ký nhận bản tin của chúng tôi.

:::note

Bạn vẫn sở hữu token xHDX mà bạn đã mua trong sự kiện Balancer LBP? Trước tiên, bạn cần [Xác nhận quyền sở hữu HDX của mình](/claim) trước khi tiếp tục.

:::

Để góp cổ phần HDX, hãy mở Polkadot/apps và kết nối với một trong các [public HydraDX RPC nodes](/polkadotjs_apps_public). Đảm bảo rằng bạn có thể thấy [số dư](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/accounts) tài khoản của mình .

:::warning

HDX token được góp cổ phần là token cổ phần để đảm bảo an ninh của mạng. Hành vi không đúng của nút xác thực mà bạn đã chỉ định có thể bị trừng phạt bằng cách cắt giảm, điều này có thể dẫn đến vô tình mất quỹ của bạn. Chúng tôi thực sự khuyên bạn nên thực hiện xét duyệt đúng đắn của mình khi chọn trình xác nhận để đề cử.

:::

Bước tiếp theo, đi đến *Network* > *Staking* > *Account actions* > *+ Stash*

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/bond-hdx-1.png')} />
</div>

Sau khi nhấp vào nút *Stash* , bạn sẽ thấy các tùy chọn góp cổ phần với bốn trường có thể chỉnh sửa:
* **stash account**: Tài khoản nắm giữ phần lớn token HDX của bạn. HDX sẽ được góp cổ phần từ tài khoản này.
* **controller account**: Tài khoản nắm giữ một phần nhỏ HDX cần để trang trải các khoản phí liên quan đến việc bắt đầu và dừng quá trình đề cử.
* **value bonded**: Số lượng HDX bạn đang góp cổ phần. Không góp cổ phần tất cả HDX mà bạn có - thay vào đó, hãy để lại một số để trang trải phí giao dịch xảy ra sau này.
* **payment destination**: Tài khoản mà phần thưởng cho trình xác thực sẽ được gửi đến.

:::warning

Không được góp cổ phần tất cả các token HDX có sẵn của bạn. Để lại một khoản dự trữ nhỏ để trang trải các khoản phí giao dịch. Nếu bạn góp cổ phần tất cả token HDX mà bạn có, bạn có thể không ký được giao dịch để bắt đầu quy trình đề cử.

:::

Sau khi điều chỉnh các tùy chọn góp cổ phần, hãy nhấp vào **Bond** và ký giao dịch để hoàn tất quá trình góp cổ phần.

:::caution

Vì lý do bảo mật, bạn không nên có cùng tài khoản Stash và Controller. Tuy nhiên, vì chuyển khoản bị vô hiệu hóa trên Snakenet, nên hiện tại không thể sử dụng các tài khoản riêng biệt. Chúng tôi thực sự khuyên bạn nên chuyển sang tài khoản Stash và Controller riêng biệt ngay khi điều này có thể thực hiện được trong tương lai.

:::

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/bond-hdx-2.png')} />
</div>

## 02 Tạo session key {#02-generate-session-keys}


Bước thứ hai là tạo session key của bạn. Các session key được sử dụng để liên kết node trình xác thực với tài khoản Controller của bạn và số HDX đã cổ phần. Do đó, điều quan trọng là chúng phải được thiết lập chính xác.

Để tạo session keys của bạn, hãy chạy lệnh sau trên node:

```bash
$ curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933

# Example output
{"jsonrpc":"2.0","result":"0x9257c7a88f94f858a6f477743b4180f0c9a0630a1cea85c3f47dc6ca78e503767089bebe02b18765232ecd67b35a7fb18fc3027613840f27aca5a5cc300775391cf298af0f0e0342d0d0d873b1ec703009c6816a471c64b5394267c6fc583c31884ac83d9fed55d5379bbe1579601872ccc577ad044dd449848da1f830dd3e45","id":1}
```

Bạn có thể tìm thấy session keys của mình trong phần _result_ của đầu ra (`0x9257...` là đầu ra trong ví dụ trên).

## 03 Thiết lập session key của bạn {#03-set-your-session-keys}

Để liên kết session keys đã tạo với tài khoản Controller của bạn, hãy điều hướng đến mục menu sau trong Polkadot/apps:
*Developer* > *Extrinsics*


Điền vào các trường:

* _using selected account_: Chọn tài khoản Controller của bạn;
* _submit the following extrinsic_: chọn `session` ở bên trái `setKeys` ở bên phải;
* _keys_: điền session keys lấy được ở bước trên vào đây;
* _proof_: `0`.

Để hoàn thành, nhấn vào _Submit Transaction_ và ký xác nhận giao dịch

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/set-session-keys-1.png')} />
</div>

## 04 Đảm bảo rằng node của bạn đã được đồng bộ hoàn toàn {#04-make-sure-that-your-node-is-fully-synced}

Trước khi tiếp tục, bạn nên đảm bảo rằng node của bạn đang chạy và quá trình đồng bộ đã hoàn tất. Cách chắc chắn nhất để kiểm tra trạng thái đồng bộ là trực tiếp trên chính node:

```bash

$ journalctl -f -u hydradx-validator.service

# The output will be similar to this
Mar 22 18:37:38 Ubuntu-2010-groovy-64-minimal hydra-dx[232761]: 2021-03-22 18:37:38  💤 
Idle (52 peers), best: #622028 (0x5f5a…1041), finalized #622025 (0x5b21…a746), ⬇ 9.1kiB/s ⬆ 6.1kiB/s

```

Bạn có thể so sánh số khối từ đầu ra (trong ví dụ trên: `# 622025`) với số khối hiện tại mà bạn có thể tìm thấy trong [Polkadot/apps Explorer](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/explorer). Tại thời điểm viết bài, khối hiện tại là `# 622240`, có nghĩa là node được sử dụng cho ví dụ này chưa được đồng bộ hoàn toàn.

Vui lòng đợi cho đến khi số khối hiển thị trong local logs của bạn khớp với số khối hiện tại của mạng.

## 05 Bắt đầu trình xác thực{#05-start-validating}

Để bắt đầu trình xác thực, hãy điều hướng trong Polkadot/apps:

*Network* > *Staking* > *Account actions* > *Validate* (nhấn next để góp cổ phẩn HDX của bạn)

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/validate-1.png')} />
</div>


Sau khi nhấp vào nút *Validate*, bạn sẽ thấy một cửa sổ bật lên có tên là *set validator preferences*. Tại đây, bạn cần đặt _reward commission percentage_ của mình. Đây là tỷ lệ phần thưởng sẽ được trả cho bạn. Phần thưởng còn lại sẽ được chia cho những người được đề cử của bạn phù hợp với số cổ phần của họ. Nếu bạn quyết định không nhận bất kỳ khoản hoa hồng thưởng nào, bạn có thể đặt tỷ lệ phần trăm thành 0.

Để xác nhận, hãy nhấp vào *Validate* và ký vào giao dịch.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/validate-2.png')} />
</div>

## 06 Kiểm tra trạng thái của node trình xác thực của bạn {#06-check-the-status-of-your-validator-node}

Bạn có thể kiểm tra trạng thái của node trình xác thực của mình trong Polkadot/apps trong:
*Network* > *Staking* > *Staking overview*

Tab này cung cấp tổng quan về tất cả các trình xác thực đang hoạt động được kết nối với mạng. Ở trên cùng, có một chỉ số về số lượng chỗ trình xác thực có sẵn, cũng như số lượng node đã trở thành một trình xác thực . Bạn có thể xác nhận xem node của mình có nằm trong hàng đợi hay không bằng cách nhấp vào tab _Waiting_.

Node trình xác thực của bạn sẽ vẫn nằm trong hàng đợi cho đến khi nó được chọn để đưa vào bộ trình xác thực. Bộ trình xác thực được cập nhật ở mỗi era điều đó cho phép thêm các node mới, miễn là có các vị trí còn trống.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/validate-3.png')} />
</div>

Cảm ơn bạn đã ủng hộ HydraDX bằng cách trở thành người xác thực Snakenet! 🎉