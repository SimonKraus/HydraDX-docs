---
id: staking
title: Staking - Góp Cổ Phần
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Phần này cung cấp một giới thiệu ngắn gọn về cách hoạt động của việc staking trong mạng HydraDX. Nếu bạn không quen với việc staking trong mạng dựa trên Substrate, chúng tôi khuyên bạn nên đọc phần này trước khi quyết định tham gia.
 
Cơ chế đồng thuận được sử dụng bởi HydraDX được gọi là Nominated Proof-of-Stake (NPoS). NPoS là một biến thể của Proof-of-Stake và được sử dụng trong các blockchain dựa trên Substrate như Polkadot và Kusama. Hai tác nhân trung tâm trong môi trường NPoS được gọi là [**Trình xác thực**](#validators) và [**Người đề cử**](#nominators).

### Trình xác thực {#validators}

Những Trình xác thực tham gia vào mạng bằng cách chạy các node trình xác thực, các node này cung cấp cơ sở hạ tầng cho phép mạng HydraDX hoạt động an toàn. Các node trình xác thực đáp ứng ba chức năng có tầm quan trọng hàng đầu đối với cơ chế đồng thuận. Chức năng đầu tiên, chúng xác thực thông tin chứa trong các khối, chẳng hạn như danh tính của các bên và chủ thể của hợp đồng. Chức năng thứ 2, các trình xác thực tham gia vào việc sản xuất các khối mới dựa trên các tuyên bố hợp lệ của các trình xác thực khác. Chức năng thứ 3, họ đảm bảo tính cuối cùng của các giao dịch blockchain.

Một đặc điểm quan trọng của NPoS là không phải tất cả các trình xác thực đều tham gia vào quá trình xác thực cùng một lúc. Chỉ những trình xác thực trong *active validator set*  mới thực hiện các hoạt động được đề cập ở trên và kiếm được [Phần thưởng](/staking_rewards) khi làm như vậy. Tập hợp các trình xác thực đang hoạt động được giới hạn ở một số node cố định. Trong [HydraDX Snakenet](/snakenet), chúng tôi mong chờ con số này sẽ vào khoảng 300, và mở rộng quy mô khi chúng tôi tiến tới mainnet.

Những trình xác thực được chọn vào nhóm hoạt động bằng cách tuân theo nguyên tắc *proportional justified representation*. Nguyên tắc này nhằm mục đích bảo vệ sự phi tập trung và đại diện công bằng bằng cách chỉ định các vị trí có sẵn cho trình xác thực theo tỷ lệ cổ phần đã được đề cử của họ. Số lượng token được góp cổ phần với trình xác thực nhất định càng cao, cơ hội node đó sẽ được chọn trong tập hợp đang hoạt động càng cao. Trình xác thực không có trong tập hợp đang hoạt động sẽ được đưa vào danh sách đợi. Tập hợp các trình xác thực đang hoạt động được cập nhật vào đầu mỗi era, cung cấp một cửa vào khả thi cho các trình xác thực mới.

:::note

Trong một mạng dựa trên Substrate, thời gian được chia thành các đơn vị được gọi là **eras**. Trong [HydraDX Snakenet](/snakenet), *1 Era = 24 giờ*.

:::

Tham gia với tư cách là một trình xác thực yêu cầu một mức độ kiến thức kỹ thuật nhất định để thiết lập và duy trì một cách an toàn Node trình xác thực. Hành vi sai trái của Node trình xác thực có thể bị trừng phạt bằng cách slashing, dẫn đến mất tiền không chủ ý cho bạn và những người đề cử cho bạn. Nếu bạn tin rằng bạn có kinh nghiệm cần thiết để chạy một Node trình xác thực, bạn có thể tham khảo [Hướng dẫn trình xác thực](/node_setup) của chúng tôi. Nếu không, chúng tôi thực sự khuyên bạn nên cân nhắc tham gia với tư cách là một người đề cử.

### Người đề cử {#nominators}

Những Người đề cử giúp bảo mật mạng bằng cách đề cử các trình xác thực đã được bầu trong tập hợp trình xác thực đang hoạt động. Họ làm như vậy bằng cách góp cổ phần HDX token của họ với các trình xác thực họ lựa chọn. Quá trình đề cử không yêu cầu chạy và duy trì các node, điều đó khiến cho hình thức góp cổ phần này dễ tiếp cận hơn với mọi người. Các token được sử dụng để để cử trình xác thực được *bonded*, có nghĩa là chúng bị đóng băng và không thể được sử dụng cho các mục đích khác. Bất cứ lúc nào cũng có thể thay đổi hoặc dừng các đề cử của bạn, điều này sẽ được phản ánh vào cuối era hiện tại. Những người đề cử cũng có thể giải phóng token của họ, tuy nhiên, điều này sẽ chỉ có hiệu lực sau khoảng thời gian chờ *28 days* sau  khi giao dịch hủy liên kết.

Trước khi đề cử, bạn phải luôn tiến hành thẩm định và nghiên cứu độ tin cậy của những trình xác nhận đã chọn. Bạn có thể làm như vậy bằng cách kiểm tra danh tính của chúng cũng như thông tin lịch sử như điểm era, lượng token được góp cổ phần , phần thưởng và slashes. Tuy nhiên, khi bắt đầu Snakenet, có thể khó tìm thấy tất cả thông tin này. Nếu bạn nghi ngờ về việc lựa chọn trình xác thực, hãy liên hệ với chúng tôi trong Discord và chúng tôi sẽ chia sẻ danh sách trình xác thực đáng tin cậy do cộng đồng tuyển chọn của chúng tôi với bạn.


Một điểm khác cần xem xét khi chọn trình xác thực là *reward commission percentage*. Điều này thể hiện tỷ lệ phần thưởng sẽ được trả cho trình xác nhận để cung cấp dịch vụ của mình cho những người được đề cử. Phần trăm hoa hồng thấp nhất không phải lúc nào cũng là tốt nhất - việc chạy một node hoạt động hiệu quả và có sẵn có chi phí hoạt động cao chỉ có thể được chi trả một cách bền vững bằng cách yêu cầu một khoản hoa hồng thưởng thực tế.

Ở HydraDX, có thể đề cử ** tối đa 16 trình xác nhận ** với cổ phần của mình. Tuy nhiên, việc đề cử nhiều hơn một trình xác thực không nhất thiết có nghĩa là cổ phần của bạn sẽ được giao cho tất cả những trình xác nhận đã chọn. Khi era tiếp theo bắt đầu, Substrate sẽ chạy một loạt các thuật toán phức tạp để xác định phân phối tối ưu nhất của tất cả các đề cử trong mạng, với mục tiêu cuối cùng là quyết định những trình xác thực nào sẽ được đưa vào tập hợp các trình xác thực đang hoạt động. Nếu không có trình xác thực nào bạn đã chọn nhận được đủ sự ủng hộ để được đưa vào nhóm đang hoạt động, ** đề cử của bạn sẽ không hoạt động ** trong khoảng thời gian era này (* 24 giờ *) và bạn cũng sẽ không nhận được phần thưởng nào trong giai đoạn này. Để tối đa hóa cơ hội đưa cổ phần của bạn vào tập hợp các trình xác thực đang hoạt động, chúng tôi đặc biệt khuyên bạn nên ** đề cử một số trình xác thực **, điều này cũng sẽ góp phần vào nỗ lực của chúng tôi trong việc nâng cao tính phi tập trung.

:::note

Đảm bảo rằng bạn không đề cử trình xác thực được đăng ký quá mức. Hiện tại, có một ** giới hạn 64 đề cử ** cho một trình xác thực duy nhất, và sau đó nó sẽ trở thành trình xác thực đã đăng ký quá mức. Khi era sau bắt đầu, trình xác thực đã đăng ký quá mức sẽ chỉ được bầu bằng cách sử dụng số lượng người được đề cử tối đa cho phép. Nếu điều này xảy ra, những người được đề cử có số cổ phần cao nhất sẽ được ưu tiên hơn, trong khi những người được đề cử có số cổ phần thấp nhất sẽ bị bỏ qua và sẽ không kiếm được bất kỳ giải thưởng nào trong era đó.

Đề cử là một hình thức góp cổ phần dễ tiếp cận hơn tuy nhiên nó cũng chịu rủi ro. Trình xác thực vi phạm các quy tắc của mạng có thể bị trừng phạt bằng cách cắt giảm, dẫn đến mất tiền cho cả người xác nhận và những người được đề cử. Đây là lý do tại sao điều quan trọng là chỉ đề cử các node trình xác nhận có uy tín.

:::

Bạn có quan tâm đến việc cổ phần HDX token của mình bằng cách đề cử người xác thực không? Xem [Hướng dẫn người đề cử ](/start_nominating) của chúng tôi để bắt đầu đề cử.
