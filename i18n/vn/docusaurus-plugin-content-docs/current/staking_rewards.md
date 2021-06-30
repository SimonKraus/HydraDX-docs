---
id: staking_rewards
title: Phần Thưởng Góp Cổ Phần
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Phần thưởng góp cổ phần là để khuyến khích trình xác nhận và người đề cử [góp cổ phần token HDX của họ] (/staking). Có ba loại phần thưởng góp cổ phần được thảo luận trong bài viết này: [phần thưởng cơ sở] (#base-rewards), [điểm era ](#era-points) and [tips](#tips).

:::note

Phần thưởng góp cổ phần không được phân phối tự động vào tài khoản của trình xác nhận và người đề cử. Thay vào đó, chúng phải được [xác nhận quyền sở hữu bằng cách kích hoạt thanh toán] (/staking_claim_rewards).

:::

## Phần thưởng cơ sở {#base-rewards}

Vào cuối mỗi era (24h), tất cả các nhóm trình xác thực đang hoạt động đều nhận được phần thưởng cơ sở dưới dạng HDX token. Một nhóm trình xác thực bao gồm trình xác thực được bầu chọn (nắm giữ HDX tự đặt cược của họ) và tất cả các đề cử đang hoạt động ủng hộ cho trình xác thực đó (để biết thêm thông tin, hãy xem [staking](/staking)). Nguyên lý trung tâm của cơ chế đồng thuận Nominated Proof-of-Stake (NPoS) là ** công việc bình đẳng mang lại phần thưởng như nhau **. Nói cách khác, vì tất cả các nhóm trình xác thực về cơ bản thực hiện cùng một công việc, ** phần thưởng cơ sở có sẵn được chia đều ** cho chúng. Điều này có nghĩa là các nhóm trình xác thực ** không ** được thưởng tương ứng với tổng số tiền đặt cược của họ, đây là sự khác biệt lớn so với các mạng PoS truyền thống.

Cơ chế chia sẻ phần thưởng cơ sở như nhau giữa tất cả các nhóm trình xác thực tham gia góp phần bảo mật mạng bằng cách ngăn chặn sự tập trung quyền lực vào một số nhóm trình xác nhận, do đó tăng cường phi tập trung hóa. Theo thời gian, nó khuyến khích những người được đề cử đề cử những trình xác nhận với số HDX đặt cược nhỏ hơn. Quá trình này cuối cùng sẽ cân bằng các mối quan hệ sức mạnh trong mạng và dẫn đến tình huống trong đó tất cả các nhóm trình xác thực đều có một lượng HDX được góp cổ phần tương đương.

Việc phân phối phần thưởng diễn ra như sau: Sau khi tính toán số phần thưởng (bằng nhau) cho mỗi nhóm trình xác thực, trình xác thực nhận được phần của nó dưới dạng ** phí hoa hồng ** để duy trì node. Ở bước thứ hai, các token còn lại được phân phối cho tất cả các HDX đã góp cổ phần ** theo tỷ lệ ** (bao gồm cả tự góp cổ phần của trình xác thực). Điều này có nghĩa là số token góp cổ phần cao hơn sẽ nhận được tỷ lệ phần thưởng lớn hơn được quy cho nhóm trình xác thực cụ thể.

:::note

Trong incentivized testnet của chúng tôi có tên là Snakenet, số lượng phần thưởng nhận được khi góp cổ phần token HDX của bạn được ước tính vào khoảng ** 50% APY **.

:::

## Điểm Era  {#era-points}

Những trình xác thực có thể kiếm được phần thưởng bổ sung tương ứng với số điểm era mà họ đã đạt được trong era trước. Những phần thưởng này được thêm vào phần thưởng cơ sở được mô tả ở trên. Trình xác thực có thể kiếm điểm era bằng cách thực hiện một số hành động cụ thể như:

* Sản xuất ra một "non-uncle block" trong Relay Chain.
* Sản xuất ra một cách giải quyết cho một "uncle block" chưa được giải quyết trước đó.
* Sản xuất ra một "referenced uncle block".

:::note

Một "uncle block" là một khối chuỗi chuyển tiếp hợp lệ trong mọi khía cạnh, tuy nhiên khối này đã không trở thành chính tắc. Điều này có thể xảy ra khi hai hoặc nhiều trình xác thực là nhà sản xuất khối trong đồng thời một khối và khối được tạo bởi một trình xác nhận đạt được là nhà sản xuất khối tiếp theo trước những người khác. Các khối trễ được gọi là khối chú - uncle block.

:::

## Tips {#tips}

Cuối cùng, trình xác nhận có thể kiếm được tiền tips cũng được thêm vào phần thưởng cơ bản vào cuối mỗi era. Tips thể hiện một khoản phí giao dịch bổ sung mà người dùng có thể tùy chọn thanh toán để giao dịch của họ có mức độ ưu tiên cao hơn.