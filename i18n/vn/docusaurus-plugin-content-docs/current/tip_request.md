---
id: tip_request
title: Yêu cầu tiền Tips từ kho bạc
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Với việc ra mắt [chương trình khuyến khích có thưởng HydraDX New Deal] (# link-to-new-deal), các thành viên cộng đồng có thể yêu cầu tiền tips HDX từ Kho bạc như một phần thưởng cho những đóng góp của họ. Hướng dẫn này sẽ hướng dẫn bạn quy trình yêu cầu tiền tips. Bạn có thể tìm thêm thông tin về các loại hoạt động nhận thưởng trong [bài đăng này](/new_deal).

Quy trình yêu cầu tips từ kho bạc bao gồm hai bước. Trong bước đầu tiên, những người đóng góp cần xuất bản yêu cầu tiền tips của họ trên Commonwealth.im cùng với mô tả về khoản đóng góp. Bước thứ hai, yêu cầu tiền tips từ kho bạc phải được gửi trực tuyến bằng Polkadot/apps.

## 01 Xuất bản yêu cầu tiền tips trên Commonwealth.im{#01-publish-tip-request}

Để bảo vệ tính minh bạch, tất cả các yêu cầu tiền tips từ Kho bạc phải được công bố bằng một bài đăng trên [trang HydraDX Commonwealth] (https://commonwealth.im/hydradx). Trước khi mở một bài đăng, bạn cần liên kết ví HydraDX của mình với Commonwealth.im: Nhấp vào *Log in* (góc trên cùng bên phải) và chọn *Connect with wallet > polkadot-js*.

<div style={{textAlign: 'center'}}>
  <img alt="login" src={useBaseUrl('/tip-request/login.jpg')} width="300px" />
</div>

Sau khi chọn địa chỉ HDX của bạn trong cửa sổ bật lên, bạn sẽ được yêu cầu ký tin nhắn bằng ví của mình và đặt tên hiển thị cho ví này.

Sau khi đăng nhập, bạn cần tạo một bài đăng mới để yêu cầu tiền tips của mình. Điều hướng đến phần trên cùng bên phải của trang và nhấp vào *New thread > New thread*. Bạn cũng có thể trực tiếp sử dụng liên kết này: https://commonwealth.im/hydradx/new/thread.

Bạn có thể sử dụng tiêu đề của bài đăng để miêu tả chủ đề (yêu cầu tiền tips) và nội dung đã đóng góp. Trong phần nội dung của bài đăng, vui lòng cung cấp thông tin sau:

* Khoảng thời gian đóng góp được thực hiện
* Tóm tắt ngắn gọn về đóng góp của bạn
* Số tiền tips được yêu cầu (bằng HDX)
* Thời gian đóng góp (tính bằng giờ)
* Nếu cần, mô tả chi tiết hơn bao gồm mức độ liên quan của khoản đóng góp cho HydraDX

Để tham khảo, bạn có thể xem qua [yêu cầu tiền tips tại ví dụ này](https://commonwealth.im/hydradx/proposal/discussion/1165-tip-request-add-documentation-for-staking).

Sau khi điền đầy đủ thông tin, hãy đăng bài đăng và nó sẽ hiển thị trong danh sách chung.

:::note

Những người đề cử và trình xác nhận đã góp cổ phần tất cả HDX của họ và bị "mắc kẹt" có thể yêu cầu tiền tips từ kho bạc là 1 HDX sẽ cho phép họ hoàn lại số cổ phần token đã góp của họ. Nếu điều này áp dụng cho trường hợp của bạn, vui lòng tạo bài đăng mới lên Commonwealth như theo [ví dụ này] (https://commonwealth.im/hydradx/proposal/discussion/1166-tip-request-overbonded-staker).

:::

## 02 Gửi yêu cầu tiền tips lên On-Chain {#02-submit-on-chain}

Sau khi xuất bản yêu cầu tiền tips từ kho bạc của bạn, bạn cần phải gửi nó trên on-chain. Với mục đích này, ví của bạn cần giữ một lượng nhỏ HDX để trang trải phí giao dịch. Nếu bạn hiện không nắm giữ bất kỳ HDX nào, bạn không cần thực hiện bước này - người khác sẽ gửi yêu cầu tiền tips lên on-chain cho bạn.

Yêu cầu tiền tips kho bạc có thể được gửi trực tuyến với Polkadot/apps bằng liên kết sau : https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/treasury/tips.

Để gửi yêu cầu tiền tips, hãy nhấp vào *Propose tip* và cung cấp thông tin sau:

* **submit with account** - chọn tài khoản sẽ ký giao dịch để gửi yêu cầu tiền tips lên on-chain. Tài khoản này cần giữ một lượng nhỏ HDX cho chi phí giao dịch.
* **beneficiary** - chọn hoặc nhập địa chỉ của tài khoản sẽ nhận được tiền tips. Tài khoản này phải tương ứng với tài khoản đã mở bài đăng trên Commonwealth.
* **tip reason** - cung cấp địa chỉ đường dẫn URL bài đăng trên Commonwealth.


<div style={{textAlign: 'center'}}>
  <img alt="login" src={useBaseUrl('/tip-request/submit-on-chain.jpg')} />
</div>

Để gửi yêu cầu tiền tips, hãy nhấp vào *Propose tip* và ký vào giao dịch.

Khi giao dịch được xác nhận, bạn sẽ thấy yêu cầu tiền tips trên trang tổng quan.

<div style={{textAlign: 'center'}}>
  <img alt="login" src={useBaseUrl('/tip-request/tip-requests.jpg')} />
</div>
