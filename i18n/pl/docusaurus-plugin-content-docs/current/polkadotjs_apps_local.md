---
id: polkadotjs_apps_local 
title: Connect to a local node 
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Możesz użyć Polkadot/app aby połączyć się z lokalnym nodem HydraDX. Aby tego dokonać, potrzebujesz mieć dostęp do portu `9944` który jest używany do połączenia RPC websocket. 

:::warning

Jeżeli jesteś walidatorem, zdecydowanie rekomendujemy umieszczenie portu `9944` na czarnej liście dla połączeń zdalnych. Potencjalni hackarzy mogą użyć tego portu aby zmiejszyć wydajność Twojego noda, co może skutkować slash'em oraz utratą części funduszy. Do połączenia ze swoim nodem walidacyjnym powinieś używać portu `9944` tylko w przypadku gdy jest on w Twojej lokalnej sieci.   

:::

### Dostęp do Twojego lokalnego noda za pomocą Polkadot/apps {#accessing-your-local-node-using-polkadotapps} 

Aby mieć dostęp do Twojego noda, otwórz [Polkadot/apps](https://polkadot.js.org/apps/) oraz użyj przycisku w lewym górnym rogu aby zmienić sieć.  

<div>
  <img src={useBaseUrl('/polkadotjs-apps/PolkadotJS-APPS-1.png')} />
</div>

Po otworzeniu się menu, kliknij na **Development** oraz wybierz **Local node**. 
<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/polkadotjs-apps/local-1.png')} />  
</div>

Zmień IP jeżeli jest to konieczne oraz kliknij na ***Switch*** aby przełaczyć się na Twój lokalny node.  

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/polkadotjs-apps/local-2.png')} />
</div>

Teraz powinieneś być połączony z Twoim lokalnym nodem oraz móc wchodzić z nim w interakcję. 
