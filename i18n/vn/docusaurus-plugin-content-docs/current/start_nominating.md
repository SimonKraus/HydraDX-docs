---
id: start_nominating
title: Trở Thành Một Người Đề Cử
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Bằng cách trở thành người đề cử, bạn góp cổ phần một số token HDX của mình để giúp bảo mật mạng HydraDX và kiếm phần thưởng. Không giống như chạy một node trình xác thực, quá trình đề cử không yêu cầu kỹ năng kỹ thuật nâng cao, làm cho nó trở thành lựa chọn được đề xuất cho bất kỳ ai không hoàn toàn tự tin với việc trở thành trình xác nhận.

Khi đề cử, những người đề cử góp cổ phần token của họ cho trình xác nhận mà họ lựa chọn. Bằng cách đó, những người đề cử sẽ chọn ra nhóm trình xác nhận đang hoạt động và nhận phần thưởng cho sự tham gia của họ. Số lượng giải thưởng bạn nhận được với tư cách là người đề cử phụ thuộc vào tỷ lệ phần trăm hoa hồng thưởng của người xác nhận đã chọn - hoa hồng thưởng của người xác nhận càng cao, bạn sẽ nhận được càng ít phần thưởng cho số token góp cổ phần của mình.

:::warning

Đề cử là một hình thức dễ tiếp cận hơn để tham gia vào quá trình góp cổ phần, tuy nhiên nó cũng mang một mức độ rủi ro nhất định. Nếu trình xác thực mà bạn đã đề cử hoạt động sai (ví dụ: không duy trì được thời gian hoạt động cần thiết), việc cắt giảm có thể xảy ra dẫn đến vô tình mất một phần token bạn đã góp cổ phần. Chúng tôi thực sự khuyên bạn nên tiến hành xét duyệt đúng đắn trước khi đề cử cho một trình xác nhận.

:::

## 00 Giao diện góp cổ phần {#00-staking-ui}

Để truy cập giao diện góp cổ phần, trước tiên bạn cần mở [Polkadot/apps](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/accounts), kết nối nó với một trong [public HydraDX RPC nodes](/polkadotjs_apps_public) và đảm bảo rằng bạn có thể thấy [số dư](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/accounts) tài khoản của mình .

:::note

Bạn vẫn sở hữu token xHDX mà bạn đã mua trong sự kiện Balancer LBP? Trước tiên, bạn cần [Xác nhận quyền sở hữu HDX của bạn](/claim) trước khi tiếp tục.

:::

Sau khi xác minh rằng bạn có thể thấy số dư HDX của mình, bạn có thể điều hướng đến Giao diện góp cổ phần:

*Network* > *Staking*

Giao diện góp cổ phần có các tab menu sau:

* **Staking overview**:  Tại đây, bạn sẽ tìm thấy danh sách tất cả các trình xác thực đang hoạt động và một số thông tin cơ bản về từng trình xác thực, chẳng hạn như số token HDX đã góp cổ phần trên node, số token góp cổ phần của chính trình xác thực và số tiền hoa hồng thưởng được tính. Hơn nữa, bạn có thể xem số điểm era mà mỗi trình xác thực kiếm được trong era hiện tại và số khối cuối cùng do trình xác thực tạo ra.
* **Account actions**: Tại đây, bạn có thể đặt góp cổ phần và đề cử
* **Payouts**: Tại đây, bạn có thể Yêu cầu phần thưởng góp cổ phần thu được của bạn
* **Targets**: Tại đây, bạn có thể ước tính thu nhập của mình. Đây là một nơi tốt để bắt đầu khi chọn một node trình xác thực để đề cử.
* **Waiting**: Tại đây, bạn có thể tìm thấy nơi xếp hàng đợi của các trình xác thực chưa hoạt động được đặt ở đây, trước khi được đưa vào tập hợp trình xác thực đang hoạt động. Một trình xác thực sẽ vẫn ở trong nơi xếp hàng đợi cho đến khi nhận được đủ số lượng HDX đã đặt cược để tham gia tập hợp trình xác thực đang hoạt động.
* **Validator stats**: Tại đây, bạn có thể truy vấn địa chỉ lưu trữ của trình xác thực để xem thông tin lịch sử chi tiết về điểm era kiếm được, số token góp cổ phần được đề cử, phần thưởng và số token bị cắt giảm. Chúng tôi thực sự khuyên bạn nên nghiên cứu thông tin này trước khi tin tưởng trình xác nhận đề cử của bạn.

## 01 Góp cổ phần HDX token {#01-bond-hdx-tokens}

:::warning

HDX token được góp cổ phần là token góp cổ phần để đảm bảo an ninh của mạng. Hành vi không đúng của node trình xác thực mà bạn đã chỉ định có thể bị trừng phạt bằng cách cắt giảm, điều này có thể dẫn đến vô tình mất quỹ của bạn. Chúng tôi thực sự khuyên bạn nên thực hiện xét duyệt đúng đắn của mình khi chọn trình xác nhận để đề cử.

:::

Để góp cổ phần HDX token , hãy điều hướng đến *Account actions* trong giao diện góp cổ phần:

*Network* > *Staking* > *Account actions* > *+ Stash*

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/bond-hdx-1.png')} />
</div>

Sau khi nhấp vào nút *Stash* , bạn sẽ thấy các tùy chọn góp cổ phần với bốn trường có thể chỉnh sửa:

* **stash account**: Tài khoản nắm giữ phần lớn token HDX của bạn. HDX sẽ được góp cổ phần từ tài khoản này.
* **controller account**: Tài khoản nắm giữ một phần nhỏ HDX cần để trang trải các khoản phí liên quan đến việc bắt đầu và dừng quá trình đề cử.
* **value bonded**: Số lượng HDX bạn đang góp cổ phần. Không góp cổ phần tất cả HDX mà bạn có - thay vào đó, hãy để lại một số để trang trải phí giao dịch xảy ra sau này.
* **payment destination**: Tài khoản mà phần thưởng góp cổ phần sẽ được gửi đến.

:::warning

Không được góp cổ phần tất cả các token HDX có sẵn của bạn. Để lại một khoản dự trữ nhỏ để trang trải các khoản phí giao dịch. Nếu bạn góp cổ phần tất cả token HDX mà bạn có, bạn có thể không ký được giao dịch để bắt đầu quy trình đề cử.

:::

Sau khi điều chỉnh các tùy chọn góp cổ phần, hãy nhấp vào **Bond** và ký giao dịch để hoàn tất quá trình góp cổ phần.

:::caution

Vì lý do bảo mật, bạn không nên có cùng tài khoản Stash và Controller. Tuy nhiên, vì chuyển khoản bị vô hiệu hóa trên Snakenet, nên hiện tại không thể sử dụng các tài khoản riêng biệt. Chúng tôi thực sự khuyên bạn nên chuyển sang tài khoản Stash và Controller riêng biệt ngay khi điều này có thể thực hiện được trong tương lai.

:::

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/bond-hdx-2.png')} />
</div>

## 02 Đề cử trình xác nhận {#02-nominate-a-validator}

Sau khi góp cổ phần HDX, bây giờ bạn có thể đề cử một trình xác thực. Trước khi tiếp tục, bạn nên thẩm định kỹ lưỡng và quyết định trình xác nhận nào bạn muốn đề cử dựa trên hiệu suất (quá khứ) của chúng. Để làm như vậy, hãy tham khảo thông tin trong Giao diện góp cổ phần [đã thảo luận ở trên] (# 00-staking-ui).

:::note

HydraDX Snakenet có một ** giới hạn 64 đề cử cho mỗi node trình xác thực **. Khi chọn một node để đề cử, hãy đảm bảo rằng trình xác nhận chưa đạt đến số lượng đề cử tối đa, nếu không đề cử của bạn sẽ không hợp lệ và bạn sẽ không nhận được phần thưởng cho số cổ phần của mình. Số lượng đề cử cho mỗi trình xác thực có thể được tìm thấy ở mục *Waiting* trong giao diện góp cổ phần.

:::

Để đề cử một hoặc nhiều trình xác thực, hãy điều hướng đến:

*Network* > *Staking* > *Account actions* > *Nominate* ( nhấn next để góp cổ phẩn HDX của bạn)

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-1.png')} />
</div>

Sau khi nhấp vào nút *Nominate*, bạn sẽ thấy một cửa sổ bật lên có tên là * đề cử trình xác nhận *. Tại đây, bạn có thể chọn một hoặc nhiều trình xác thực để đề cử từ danh sách các trình xác nhận có sẵn. Bạn nên chỉ định nhiều trình xác thực để tránh việc không hoạt động nếu bạn không có được vị trí trong một trình xác thực (ví dụ: trình xác thực quá đông hoặc không được chọn vào tập hợp trình xác thực đang hoạt động). Bạn có thể đề cử tối đa 16 trình xác nhận. Trong mỗi era, chỉ một trong số các đề cử của bạn có thể hoạt động, bạn không thể được chọn bởi nhiều trình xác nhận cùng một lúc. Cổ phần của bạn sẽ tự động được chỉ định cho một trong những trình xác nhận đã chọn của bạn theo cách để tối đa hóa sự phi tập trung và lợi nhuận. Bạn chỉ cần chọn số lượng HDX đã được góp cổ phần và trình xác thực mà bạn tin tưởng.

Để đề cử trình xác thực đã chọn, hãy nhấp vào _Nominate_ và ký giao dịch.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-2.png')} />
</div>


## 03 Kiểm tra trạng thái đề cử của bạn {#03-check-the-status-of-your-nominations}


Để kiểm tra trạng thái của các đề cử của bạn, hãy điều hướng đến:

*Network* > *Staking* > *Account actions*

Bạn có thể thấy các đề cử không hoạt động của mình trong *Waiting nominations*:

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-3.png')} />
</div>

Khi một đề cử có hiệu lực, bạn sẽ tìm thấy nó trong danh sách *Active nominations*

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-4.png')} />
</div>  

:::note

Đảm bảo rằng bạn thỉnh thoảng xem lại các đề cử của mình. Có thể một số trình xác thực của bạn thay đổi tỷ lệ phần trăm hoa hồng của chúng, điều này sẽ có tác động tiêu cực đến phần thưởng của bạn. Bằng cách kiểm tra trạng thái của các đề cử của bạn thường xuyên, bạn sẽ có thể phản ứng bằng cách cập nhật danh sách những trình xác thực được đề cử của bạn.

:::

## 04 Điều chỉnh các đề cử của bạn {#04-adjust-your-nominations}

Nếu một số trình xác thực của bạn đăng ký quá mức hoặc thay đổi hoa hồng của chung, bạn có thể muốn điều chỉnh các đề cử của mình.

Để làm như vậy, hãy mở Polkadot/apps và điều hướng đến:  

*Network* > *Staking* > *Account actions*

Nhấp vào dấu ba chấm bên cạnh chi tiết tài khoản của bạn và chọn _Set nominees_.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-set-nominees.png')} />
</div>

Cửa sổ sau đó, có thể bạn đã cảm thấy quen thuộc, bạn có thể xóa trình xác thực và / hoặc thêm trình xác thực mới.

Điều chỉnh đề cử của bạn có thể được thực hiện nhanh chóng, không cần phải dừng đề cử. Các thay đổi sẽ được áp dụng khi era sau bắt đầu (24h)

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-2.png')} />
</div>  

## 05 Hoàn lại quỹ góp cổ phần {#05-rebond-funds}

Nếu bạn đã vô tình hủy góp cổ phần token HDX của mình, bạn có thể góp cổ phần lại chúng trước khi khoảng thời gian chờ 28 ngày hết hiệu lực.

Để làm như vậy, hãy mở Polkadot/apps và điều hướng đến *Developer* > *Extrinsics* . Ngoài ra, bạn có thể truy cập liên kết này:
https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/extrinsics


Chọn tài khoản của bạn bằng nút thả xuống trong " using the selected account" . Sau đó, bạn cần điền các thông tin sau:
* **extrinsic**: staking
* **action**: rebond_value
* **value**: ở đây bạn cần nhập số lượng HDX bạn muốn hoàn lại quỹ góp cổ phần.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/rebond.png')} />
</div>


Nếu mọi thứ được đặt chính xác, bạn có thể gửi extrinsic đó bằng cách nhấp vào nút _Submit Transaction_ và ký giao dịch trong tiện ích mở rộng Polkadot.js. Sau khi hoàn tất, lượng HDX đã chọn sẽ được góp cổ phần hoàn lại.

Cảm ơn bạn đã ủng hộ HydraDX bằng cách trở thành người đề cử Snakenet! 🎉