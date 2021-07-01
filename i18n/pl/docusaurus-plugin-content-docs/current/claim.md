---
id: claim
title: Claim your HDX
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Możesz odebrać swoje HDX za pomocą tokenów xHDX (ERC-20), które otrzymałeś w czasie działania naszego [Balancer LBP](https://hydradx.substack.com/p/lbp-announcement).

:::note

Nie posiadasz żadnych tokenów xHDX, ale mimo to chcesz otrzymać trochę HDX? Dziękujemy za zainteresowanie, ale w tej chwili nie ma możliwości zakupu tokenów HDX - transfery HDX są zamrożone aż do sieci mainnet. Jednak w miarę zbliżania się do sieci mainnet będziemy uruchamiać programy motywacyjne dla społeczności, dzięki którym można zarobić trochę wczesnego HDX. Jeśli jesteś zainteresowany, [zapisz się do naszego newslettera](https://hydradx.substack.com) i dołącz do naszego serwera Discord, aby być na bieżąco.

:::

## Wymagania wstępne {#prequisites}

Są dwa warunki wstępne, które należy spełnić, aby odebrać HDX. W pierwszej kolejności musisz zainstalować [rozszerzenie przeglądarki Polkadot.js](https://polkadot.js.org/extension/) które posłuży do stworzenia Twojego portfela HDX. W drugiej kolejności, potrzebujesz dostępu do swoich tokenów xHDX, które powinny być przechowywane w portfelu wspierającym podpisywanie wiadomości dotyczących tokenów ERC-20 (np. Metamask).

Jeśli twoje tokeny xHDX są przechowywane w Coinbase Wallet lub Trust Wallet, będziesz musiał skorzystać z jednego z poniższych rozwiązań, aby odebrać swóje HDX, ponieważ te portfele nie obsługują podpisywania wiadomości:
* Metamask: Możesz użyć rozszerzenia przeglądarki Metamask i zaimportować swój portfel, używając seed-phrase.
* MEW (MyEtherWallet): Możesz również użyć MEW, importując swoje seedy lub skorzystać z bespośrenio z połączenia WalletLink. Dostęp do obu opcji można uzyskać za pomocą strony [MyEtherWallet](https://www.myetherwallet.com/access-my-wallet). Jeśli korzystasz z portfela Coinbase, możesz użyć WalletLink, w którym znajdziesz ustawienia portfela Coinbase.

## Proces odbioru tokenów {#claim-process}

Po upewnieniu się, że spełnione zostały wymagania wstępne opisane powyżej, możesz przejść do  [HydraDX Claim app](https://claim.hydradx.io) i kontynuować proces odbierania HDX.

Podczas procesu zebrania wykorzystasz swoje tokeny xHDX (ERC-20), aby odebrać swoją część tokenów HDX.

### 00 Autoryzacja {#00-authorize}

Aplikacja HydraDX Claim zażąda autoryzacji z rozszerzenia przeglądarki Polkadot.js

:::warning

Upewnij się, że nie jesteś ofiarą ataku phishingowego i zwróć uwagę na wyskakujące okienko autoryzacji: aplikacja powinna identyfikować się jako CLAIM.HYDRADX.IO, a żądanie powinno pochodzić z **https://claim.hydradx.io**.

:::

<img alt="authorize" src={useBaseUrl('/claim/authorize.jpg')} />

Po autoryzacji zostanie wyświetlone okno do zaktualizowania meta danych w rozszerzeniu przeglądarki Polkadot.js. Umożliwi to Polkadot.js utworzenie adresów charakterystycznych dla HydraDX, które są wymagane do zakończenia procesu zbierania tokenów.

<img alt="authorize" src={useBaseUrl('/claim/metadata.jpg')} />

### 01 Wybierz swój adres ETH {#01-select-your-eth-address}

W pierwszym etapie procesu zbierania zostaniesz poproszony o wybranie konta, na którym znajdują się Twoje tokeny xHDX. Można to zrobić, łącząc się z portfelem zawierającym tokeny ERC-20 (np. Metamask) lub wpisując ręcznie swój adres ETH w polu wprowadzania (w takim przypadku konieczne będzie później ręczne podpisanie wiadomości).

Po wprowadzeniu adresu ETH powinieneś zobaczyć saldo tokenów HDX, które możesz odebrać, w tym [refundację opłaty za gas](https://hydradx.substack.com/p/first-governance-vote) który wydałeś na uzyskanie xHDX na Balancer.

:::note

Nie kwalifikujesz się do zwrotu gasu, jeśli uzyskałeś xHDX w innym miejscu niż oficjalny pool Balansera (na przykład Uniswap) lub jeśli przeniosłeś swoje tokeny z portfela, z którego dokonano zakupu.

:::

<img alt="authorize" src={useBaseUrl('/claim/claim-01.jpg')} />

### Utwórz i wybierz adres HDX {#02-create-and-select-an-hdx-address}

W drugim kroku zostaniesz poproszony o wybranie adresu HDX.

Aby utworzyć nowy adres HDX, otwórz rozszerzenie przeglądarki Polkadot.js i kliknij znak +, aby utworzyć nowe konto. Na pierwszym etapie tworzenia konta zobaczysz 12-wyrazów seed-phrase, który może zostać użyty do odzyskania Twojego konta. Po zapisaniu seed-phrase w bezpiecznym miejscu, kliknij *Next step*. W tym miejscu należy zmienić sieć (**Network**) poprzez wybranie **HydraDX Snakenet**. Wprowadź nazwę i hasło do swojego konta i zakończ tworzenie konta.

<img alt="authorize" src={useBaseUrl('/claim/create-account.png')} />

:::warning 

Upewnij się, że utworzyłeś kopię zapasową seed-phrase i przechowujesz ją w bezpiecznym miejscu, nigdy nikomu nie udostępniając. Wykorzystanie seed-phrase to jedyny sposób w jaki możesz odzyskać swoje konto, więc jeśli ją zgubisz lub zostanie Ci skradziona, stracisz swoje fundusze. Pamiętaj, że musisz zabezpieczyć dostęp do tego portfela aż do momentu uruchomienia sieci mainnet, ponieważ wszystkie salda HDX są obecnie zablokowane. Jeśli stracisz dostęp do swojego portfela HDX, utracisz również swój HDX.

:::

Po utworzeniu konta HDX powinieneś mieć możliwość wybrania go w aplikacji HydraDX Claim. Po wykonaniu tej czynności, w aplikacji powinieneś uzyskać podgląd adresów ETH i HDX używanych w procesie zbierania tokenów. Kliknij Dalej, aby przejść do podpisania wiadomości.

<img alt="authorize" src={useBaseUrl('/claim/claim-02.jpg')} />

### 03 Podpis {#03-sign}

W trzecim etapie procesu zbierania za pomocą aplikacji HydraDX Claim, otrzymasz możliwość podpisania wiadomości o użyciu tokenów xHDX w celu odebrania HDX.

:::note

Pamiętaj, że w tym kroku zobaczysz klucz publiczny (**public key**) swojego adresu HDX, nie będzie to adres w czytelnej dla człowieka formie, tak jak był w poprzednim kroku oraz w rozszerzeniu przeglądarki Polkadot.js (więcej szczegółów znajdziesz w [ss58 docs](https://polkadot.js.org/docs/keyring/start/ss58 )). Jeśli wykonałeś wszystkie kroki opisane powyżej, nie ma się czym martwić i można bezpiecznie przystąpić do podpisania wiadomości. Sprawdzimy również, czy konto HDX, którego używasz do podpisania transakcji odebrania na ostatnim etapie, jest zgodne z kontem, które zostało podane do odebrania tokenów HDX.

:::

W zależności od wyboru dokonanego w pierwszym kroku, masz dwie możliwości podpisania wiadomości o wykorzystaniu tokenów xHDX w procesie odbierania:

* Jeśli używasz **Metamask**, po kliknięciu przycisku Podpisz zostaniesz poproszony przez Metamask o podpisanie wiadomości. Postępuj zgodnie z instrukcjami w Metamask.
* Jeśli podałeś swój adres ETH ręcznie, będziesz musiał podpisać wiadomość za pośrednictwem zewnętrznego portfela, w którym znajdują się klucze prywatne Twoich tokenów xHDX. Po podpisaniu wiadomości skopiuj podpis (zaczynając od 0x ) do odpowiedniego pola w aplikacji HydraDX Claim.

<img alt="authorize" src={useBaseUrl('/claim/claim-03.jpg')} />

### 04 Claim {#04-claim}

Po podpisaniu wiadomości z portfelem zawierającym tokeny xHDX, powinno otworzyć się rozszerzenie Polkadot.js i zostaniesz poproszony o podpisanie transakcji w celu odebrania HDX na swoje konto. Wprowadź hasło do konta HDX i kliknij *Sign the transaction*.

<img alt="authorize" src={useBaseUrl('/claim/claim-sign.jpg')} />

Zakończyłeś proces zebrania, tym samym oficjalnie stając się właścicielem HDX!

Możesz sprawdzić saldo za pomocą [Polkadot/apps](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/accounts) podłączonych do sieci HydraDX Snakenet. Pamiętaj, że nie możesz zobaczyć salda HDX bezpośrednio w rozszerzeniu przeglądarki Polkadot.js. 

### 05 Następne kroki {#05-whats-next}

Po zakończeniu procesu zebrania tokenów HDX pozostaną one zablokowane w Twoim portfelu aż do czasu uruchomienia sieci mainnet. 

Z drugiej strony tokeny xHDX (które wykorzystałeś do odebrania HDX) pozostaną zablokowane na Twoim portfelu ERC-20 na zawsze, co oznacza, że możesz je ukryć na swoim portfelu (lub zachować je widoczne jako odznaka wczesnego użytkownika).

Chcesz wykorzystać swoje tokeny HDX do pracy i pomóc poprawić bezpieczeństwo sieci HydraDX? Jeśli tak, możesz wziąć udział w naszej motywującej sieci testowej o nazwie **Snakenet** stakując swoje HDX. Jeśli jesteś zainteresowany, możesz kontynuować, zapoznając się z  [procesem stakowania](/staking), , po którym możesz zdecydować się na udział jako [walidator](/start_validating) lub [nominator](/start_nominating).
