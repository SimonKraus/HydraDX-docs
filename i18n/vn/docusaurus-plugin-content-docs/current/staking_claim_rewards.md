---
id: staking_claim_rewards
title: Yêu cầu phần thưởng góp cổ phần thu được của bạn
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Vào cuối mỗi era, các nhóm trình xác thực được chia phần [staking rewards](/staking_rewards) của họ, bao gồm phần thưởng cơ bản, phần thưởng điểm era và tips. Tuy nhiên, những phần thưởng này không được phân phối tự động vào tài khoản của trình xác nhận và những người được đề cử. Điều này sẽ chỉ xảy ra sau khi phần thưởng góp cổ phần đã được xác nhận bằng cách ** kích hoạt thanh toán **. Phần thưởng góp cổ phần phải được xác nhận ** trong vòng 84 eras ** sau khi đã kiếm được. Sau khi khoảng thời gian này kết thúc, thông tin phần thưởng có liên quan sẽ bị xóa khỏi chuỗi và nhóm trình xác nhận không còn có thể nhận phần thưởng cho era đó nữa.

Quá trình kích hoạt thanh toán theo cách thủ công trong một khung thời gian giới hạn là một tính năng bảo mật quan trọng. Bằng cách yêu cầu giao dịch thanh toán được gửi cho mọi nhóm trình xác thực và cho mỗi era, việc phân phối phần thưởng được trải rộng trên nhiều khối. Nếu tất cả phần thưởng được phân phối cho tất cả trình xác nhận và người đề cử trong một khối duy nhất, thì sự ổn định của chuỗi có thể bị đe dọa.

## Cách kích hoạt thanh toán

Thanh toán có thể được kích hoạt dễ dàng bởi cả trình xác nhận và người đề cử của họ bằng Polkadot/apps. Để làm điều đó, hãy điều hướng đến *Network > Staking > Payouts*. Ngoài ra, bạn có thể sử dụng liên kết sau:
https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/staking/payout

Khi chọn *My stashes*, bạn sẽ thấy tất cả các phần thưởng có sẵn để thanh toán cho các token đã đặt cược của bạn với chỉ báo về số era tương ứng. Bằng cách nhấp vào *Payout all*, bạn có thể gửi một loạt giao dịch để yêu cầu tất cả các phần thưởng có sẵn cho các era trước đây.
<img src={useBaseUrl('/staking-claim-rewards/payouts.jpg')} />

Sau khi kích hoạt thanh toán, bạn sẽ được yêu cầu ký (các) giao dịch bằng tài khoản HDX của mình. Sau khi được xác nhận, phần thưởng cho các eras đã chọn sẽ được phân phối cho những trình xác nhận tương ứng và những người đề cử của họ.