---
id: start_validating 
title: Become a validator
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Po skonfigurowaniu [węzła](/node_setup), przed rozpoczęciem walidacji, wymagane jest zablokowanie tokenów (ang. Token Bonding) HDX i ustanowienie klucza dostępowego dla węzła.

:::warning

Prowadzenie Węzła Walidującego (ang. Validator Node) wymaga specyficznych umiejętności technicznych, potrzebnych do początkowej konfiguracji węzła oraz zapewnienia późniejszej gwarancji ciągłości jego działania. Od walidatorów, wymagamy korzystania z ostatniego stabilnego wydania naszego oprogramowania. Jeśli nie do konca jesteś pewien, co tutaj robisz, zalecamy [nominowanie swoich tokenów](/start_nominating) bardziej doświadczonemu walidatorowi.
Wybierając tą ścieżkę, chronisz siebie oraz osoby Ciebie nominujące, przed przypadkową, nieodwracalną utratą środków


:::

## 01 Zablokowanie tokenów {#01-bond-hdx-tokens}

Aby zostać częscią sieci jako walidator, wymagane jest zablokowanie tokenów HDX. Osoby obecnie ich nie posiadające, nie będą miały możliwości brania udziału w pierwszej fazie testnet. Nowe, ekscytujące newsy i informacje dotyczące projektu uwalniane będą przez załogę HDX w przeciągu najbliższych tygodni. Zapraszamy do śledzenia naszych mediów oraz do zapisów do newslettera. 

:::note

Jeśli w dlaszym ciągu jesteś w posiadaniu tokenów xHDX, kupionych na Balancer LBP , skieruj się na poniższa stronę aby je [odebrać](/claim).

:::

Aby zablokować HDX, otwórz Polkadot/apps, oraz połącz sie z jednym z [publicznych wezłów RPC](/polkadotjs_apps_public). Upewnij się, że balans twojego konta widoczny jest pod [tym adresem](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/accounts).

:::warning

Zablokowane tokeny HDX, grają bardzo ważną rolę w zwiększaniu poziomu bezpieczeństwa sieci.
Nieprawidłowe zachowania na poziomie węzła walidującego mogą zostać ukarane poprzez proces karania (ang. Slashing), który może doprowadzic do utraty środków operatora węzła. 

Szczerze polecamy, aby na tym etapie, kontynuować tylko i wyłącznie, jeśli jesteś pewien, że wiesz co robisz.

:::

Jako następny krok, udaj się do  *Network* > *Staking* > *Account actions* > *+ Stash*

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/bond-hdx-1.png')} />
</div>

Po kliknieciu „Stash”, powinienes zobaczyć stronę ustawień powiązywania tokenów HDX z czterema polami do edycji:
* **stash account**: konto utrzymujące większość twoich tokenów HDX. Twoje tokeny HDX będą stakowane z tego konta.
* **controller account**: konto utrzymujące mniejszą ilość Twoich tokenów HDX, wymaganych do pokrywania kosztów rozpoczynania i kończenia procesu walidacji.
* **value bonded**: Ilość tokenów HDX obecnie zablokowanych przez użytkownika. Zwróć uwagę, żeby nie wiązać (ang. Bond) wszystkich dostępnych tokenów HDX. Upewnij się, że część z nich jest zawsze dostępna na pokrycie kosztów transakcji, które pojawią się w przyszlości
* **payment destination**: Konto, na które wypłacane będą nagrody za prowadzenie węzła walidacyjnego.

:::warning

Nie blokuj (ang. Bond) wszystkich dostępnych tobie tokenów HDX. 
Upewnij się, że mała część z nich jest zawsze dostępna na pokrycie kosztów transakcji.
Jeśli powiążesz wszystkie swoje tokeny, możesz nie być w stanie opłacić kosztów wysłania transakcji wymaganej do rozpoczęcia procesu walidacji.

:::

Po odpowiednim ustawieniu wartości w polach do edycji, naciśnij _Bond_) i zatwierdź transakcję w celu zakończenia procesu powiązywania tokenów.

:::caution

Ze wzgledów bezpieczeństwa, polecamy nie używanie tego samego konta dla "Stash" i "Controller". Niestety, z powodu wstrzymania transferów na sieci Stakenet, obecnie nie jest możliwe rozdzielenie tych 2 kont. Polecamy zmiane na oddzielne konta jak tylko ta opcja znów stanie się dostępna.

:::

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/bond-hdx-2.png')} />
</div>

## 02 Generowanie klucza sesji {#02-generate-session-keys}

Kolejnym krokiem do podjęcia jest wygenerowanie klucza sesji. Klucz sesji stosowany jest do późniejszego powiązania węzła walidującego z odpowiednim kontem "Controller" i powiązanymi tokenami HDX. Dlatego też jest to bardzo ważne, aby ustawienia te były poprawne.

Aby wygenerować klucz sesji, na Twoim węźle uruchom:

```bash
$ curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933

# Example output
{"jsonrpc":"2.0","result":"0x9257c7a88f94f858a6f477743b4180f0c9a0630a1cea85c3f47dc6ca78e503767089bebe02b18765232ecd67b35a7fb18fc3027613840f27aca5a5cc300775391cf298af0f0e0342d0d0d873b1ec703009c6816a471c64b5394267c6fc583c31884ac83d9fed55d5379bbe1579601872ccc577ad044dd449848da1f830dd3e45","id":1}
```

Możesz znaleść Twoje klucze sesji w części _result_  (`0x9257...` w powyższym przykładzie).

## 03 Ustawienie kluczy sesji {#03-set-your-session-keys}

W celu połączenia wygenerowanego klucza sesji z kontem „Controller Account” przejdz do:
*Developer* > *Extrinsics*

Oraz wypełnij pola:

* _using selected account_: wybierz Twoje konto "Controller";
* _submit the following extrinsic_: wybierz `session` w lewym panelu oraz `setKeys` po prawej;
* _keys_: wprowadz swóje klucze sesji, wygenerowane w poprzednim kroku;
* _proof_: `0`.

W celu ukończenia procesu, kliknij _Submit Transaction_ oraz podpisz transakcję.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/set-session-keys-1.png')} />
</div>

## 04 Upewnij się że twój węzej jest w pełni zsynchronizowany {#04-make-sure-that-your-node-is-fully-synced}

Przed podjęciem nastepnych kroków, upewnij się, że Twój węzeł walidacyjny działa oraz proces synchronizacji został zakończony. Najłatwiejszą metodą upewnienia się jest wysłanie zapytania z poziomu węzła:

```bash

$ journalctl -f -u hydradx-validator.service

# The output will be similar to this
Mar 22 18:37:38 Ubuntu-2010-groovy-64-minimal hydra-dx[232761]: 2021-03-22 18:37:38  💤 
Idle (52 peers), best: #622028 (0x5f5a…1041), finalized #622025 (0x5b21…a746), ⬇ 9.1kiB/s ⬆ 6.1kiB/s

```

Po uzyskaniu odpowiedzi, zgodność sprawdzić możesz porównując przedstawiony pole block-number (w powyższym przypadku : `#622025`) z obecnym przetwarzanym numerem bloku dostępnym na  [Polkadot/apps Explorer](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/explorer). W momencie pisania artykułu obecny numer bloku to `#622240`, co znaczy, że węzeł użyty w naszym przykładzie nie jest w pełni zsynchronizowany.

W takim przypadku, odczekaj do momentu, az number bloku z logów obsługiwanego przez Ciebie węzłą, zgadzać się będzie z obecnym numerem bloku sieci.

## 05 Start walidacji {#05-start-validating}

Aby rozpocząć walidację, w aplikacji Polkadot/apps wybierz:

*Network* > *Staking* > *Account actions* > *Validate* 

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/validate-1.png')} />
</div>

Po wybraniu opcji „Validate” powinieneś zobaczyc okno „set validator preferences”.
Tutaj, wymagane jest ustalenie wartości procentowej nagród. Jest to proporcja nagród, które wypłacane bedą tobie, jako operatorowi węzła. Reszta nagród wypłacana będzie użytkownikom, którzy nominowali twojemu węzłowi swoje tokeny, proporcjonalnie do udziału w puli.
Jeśli zdecydujesz się nie otrzymywać żadnych nagród za prowadzenie węzła, wartośc ustawić możesz na 0%.

W celu potwierdzenia, kliknij „Validate” oraz zatwierdź transakcję.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/validate-2.png')} />
</div>

## Sprawdź status swojego węzła walidacyjnego {#06-check-the-status-of-your-validator-node}

Możesz sprawdzić stan swojego węzła walidacyjnego w Polkadot/apps:

*Network* > *Staking* > *Staking overview*

Ta zakladka dostarczy ci informacji na temat wszystkich aktywnych węzłów podłączonych do sieci. Na górze, znajdziesz ilość dostępnych miejsc na węzły walidacyjne, jak również ilość węzłów zgłoszonych chęć zostania walidatorem. Miejsce w kolejce do zostania walidatorem zajęte przez twój węzeł możesz potwierdzić klikając w zakładkę _Waiting_ .

Twój węzeł zostanie w kolejce do momentu, aż wybrany zostanie do dołaczenia do zestawu walidatorów. Zestaw walidatorów uaktualniany jest w każdej erze, co pozwala na dołączanie nowych węzłów, jeśli są dla nich wolne miejsca.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/validator-guide/validate-3.png')} />
</div>

Dziękujemy za wsparcie HydraDX poprzez zostanie walidatorem Stakenet! 🎉
