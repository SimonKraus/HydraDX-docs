---
id: polkadotjs_apps_local 
title: Kết Nối Tới Local Node 
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Bạn có thể sử dụng Polkadot/apps để kết nối với local HydraDX node của mình. Với mục đích này, bạn cần có quyền truy cập vào cổng `9944` được sử dụng cho các kết nối websocket RPC.

:::warning
Nếu bạn đang chạy node với tư cách là Trình xác thực, chúng tôi thực sự khuyên bạn nên đưa cổng `9944` vào danh sách đen cho các kết nối từ xa. Cổng này có thể bị lạm dụng bởi các bên thứ ba để làm giảm hiệu suất của node, điều này có thể dẫn đến việc slashing và mất tiền một cách không chủ ý. Bạn chỉ nên sử dụng cổng `9944` để kết nối với nút trình xác thực khi nút đó nằm trong mạng Local của bạn.
:::

### Truy cập vào Local Node của bạn bằng Polkadot/apps {#accessing-your-local-node-using-polkadotapps}

Để truy cập vào Node của bạn, hãy mở [Polkadot/apps](https://polkadot.js.org/apps/) và nhấp vào ở góc trên bên trái để thay đổi mạng.

<div>
  <img src={useBaseUrl('/polkadotjs-apps/PolkadotJS-APPS-1.png')} />
</div>

Sau khi mở menu, nhấp vào **Development** và chọn **Local node**.
<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/polkadotjs-apps/local-1.png')} />
</div>

Điều chỉnh IP nếu cần và nhấp vào ***Switch*** để chuyển sang Local Node của bạn local node.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/polkadotjs-apps/local-2.png')} />
</div>

Bây giờ bạn sẽ được kết nối với Local Node của mình và có thể tương tác với nó.