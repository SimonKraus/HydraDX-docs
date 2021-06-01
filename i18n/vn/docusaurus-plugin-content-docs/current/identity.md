---
id: identity
title: Thiết lập danh tính của bạn
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Chủ tài khoản có khả năng thiết lập danh tính của họ bằng cách cung cấp thông tin cụ thể và lưu trữ nó trên on-chain. Bên cạnh đó, thông tin nhận dạng có thể được tùy chọn gửi đến các nhà đăng ký HydraDX để xác minh. Bằng cách thiết lập và xác minh danh tính của họ, các trình xác thực và người đề cử giúp bảo vệ sự tin cậy trong mạng.

:::note
Nếu bạn đang tham gia với tư cách là một trình xác thực HydraDX , chúng tôi **thực sự khuyên** bạn nên đặt cả danh tính của mình và trải qua quá trình xác minh. Những trình xác thực đã được xác minh có vẻ đáng tin cậy hơn và thu hút nhiều người đề cử hơn, do đó tăng cơ hội được đưa vào nhóm trình xác thực đang hoạt động.
:::

## 01 Thiết lập danh tính {#01-set-identity}

Để thiết lập danh tính, mở Polkadot/apps ( kết nối tới mạng *HydraDX Snakenet* ) và điều hướng tới *My accounts*. Ngoài ra, bạn có thể truy cập liên kết này:
https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/accounts

Trên trang tài khoản, hãy tìm tài khoản đang giữ  HDX tokens đã được góp cổ phần của bạn. Sau đó, nhấp vào ba dấu chấm bên cạnh tài khoản (ở phía bên phải) và chọn *Set on-chain identity*.

<img alt="authorize" src={useBaseUrl('/identity/set-identity-1.jpg')} />

Bạn sẽ thấy một cửa sổ bật lên có tên là *register identity*. Tại đây, bạn có thể nhập các thông tin sau:

* Tên của bạn
* email
* Địa chỉ website
* Tài khoản twitter của bạn
* riot name (Trong trường hợp bạn sử dụng Matrix messaging)

:::note

Tất cả thông tin này là tùy chọn - vui lòng chỉ cung cấp các chi tiết bạn chọn. Tuy nhiên, nếu bạn đang chạy một node trình xác thực, chúng tôi khuyên bạn nên đặt email của mình . Điều này sẽ cho phép chúng tôi liên hệ với bạn trong trường hợp chúng tôi gặp sự cố với node của bạn.

:::

Trong trường dữ liệu cuối cùng của cửa sổ bật lên, bạn có thể thấy số lượng HDX bạn cần nạp để lưu trữ thông tin nhận dạng của mình. Bạn sẽ nhận lại khoản tiền gửi này sau khi bạn quyết định xóa danh tính của mình vào thời điểm sau đó.

<img alt="authorize" src={useBaseUrl('/identity/set-identity-2.jpg')} />

Sau khi điền đầy đủ thông tin, hãy nhấp vào *Set Identity* và ký giao dịch bằng tiện ích mở rộng trình duyệt Polkadot.js. Một khi giao dịch được xác nhận, danh tính của bạn đã được thiết lập.

## 02 Gửi danh tính của bạn để xác minh {#02-verify-identity}

Sau khi bạn đã thiết lập danh tính của mình, bạn có thể gửi danh tính cho nhà đăng ký mạng để xác minh. Để làm như vậy, hãy mở Polkadot/apps và điều hướng đến *Developer* > *Extrinsics*.Ngoài ra, bạn có thể truy cập liên kết này:
https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/extrinsics

Sau khi chọn tài khoản HydraDX phù hợp từ bước cuối cùng, bạn cần điền các thông tin sau: 

* **extrinsic**: identity
* **action**: requestJudgement
* **reg_index**: bạn cần nhập ID của nhân viên đăng ký mà bạn chọn để thực hiện xác minh ở đây.
HydraDX có 2 nhân viên đăng ký: Simon Kraus - HydraSik (ID: **0**) và Jimmy Tudeski - stakenode (ID: **1**).
* **max_fee**: bạn cần nhập khoản phí tối đa bằng HDX mà bạn sẵn sàng trả cho nhân viên đăng ký để xác minh ở đây. Chỉ những nhân viên đăng ký có mức phí dưới max_fee của bạn mới đủ điều kiện để thực hiện xác minh.

Để gửi yêu cầu xác minh của bạn, hãy nhấp vào *Submit Transaction*  và ký vào giao dịch.

<img alt="authorize" src={useBaseUrl('/identity/set-identity-3.jpg')} />

Xin lưu ý rằng quá trình xác minh danh tính có thể mất một khoảng thời gian để hoàn thành. Để xem trạng thái yêu cầu của bạn, hãy điều hướng đến  **My accounts** và di chuột qua phần hiển thị danh tính của bạn - bạn sẽ thấy một cửa sổ bật lên hiển thị trạng thái hiện tại.

## 03 Outcome of the verification procedure {#03-verification-outcome}

Sau khi xử lý yêu cầu xác minh của bạn, Nhân viên đăng ký sẽ gửi một trong các phán quyết sau sẽ hiển thị trong trạng thái danh tính của bạn:

* **Unknown** - giá trị mặc định, chưa có phán quyết nào được đưa ra.
* **Reasonable** - thông tin được cung cấp có vẻ hợp lý, tuy nhiên không có kiểm tra chuyên sâu nào được thực hiện.
* **KnownGood** - thông tin chính xác.
* **OutOfDate** - thông tin trước đây chính xác nhưng bây giờ nó đã lỗi thời.
* **LowQuality** - thông tin không chính xác nhưng nó có thể được sửa chữa bằng cách cập nhật nó.
* **Erroneous** - thông tin được cung cấp là sai và có thể xác định là một ý định xấu.
