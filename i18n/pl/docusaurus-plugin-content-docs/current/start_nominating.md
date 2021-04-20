---
id: start_nominating
title: Become a nominator
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Stając się nominującym, przeznaczasz część swoich tokenów HDX na pomoc w zabezpieczeniu sieci HydraDX oraz na nagrody. W przeciwieństwie do prowadzenia noda walidatora, proces nominowania nie wymaga zaawansowanych umiejętności technicznych, co sprawia, że jest to zalecany wybór dla każdego, kto nie jest w pełni przekonany do zostania walidatorem.

Nominując, nominujący przydzielają swój udział wybranemu przez siebie walidatorowi. W ten sposób nominujący wybierają aktywny zestaw walidatorów i otrzymują nagrody za swój udział. Ilość nagród, które otrzymasz jako nominator zależy od procentowej prowizji od nagrody wybranego walidatora - im wyższa prowizja od nagrody walidatora, tym mniej nagród otrzymasz za swój udział.

:::warning

Nominowanie jest bardziej przystępną formą uczestnictwa w procesie stakingu, jednak niesie ze sobą również pewien stopień ryzyka. Jeśli nominowany przez Ciebie walidator nie będzie działał prawidłowo (np. nie będzie utrzymywał wymaganego czasu pracy), może dojść do slashingu, który może doprowadzić do częściowej utraty postawionych przez Ciebie środków. Gorąco zalecamy, abyś dołożył należytej staranności przed nominowaniem walidatora.

:::

## 00 Staking UI {#00-staking-ui}

Aby uzyskać dostęp do interfejsu stakowania, musisz najpierw otworzyć aplikację Polkadot/apps, połączyć się z jednym z [publicznych nodów](/polkadotjs_apps_public) i upewnić się, że możesz zobaczyć stan [swojego konta](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc-01.snakenet.hydradx.io#/accounts)

:::note

Czy nadal jesteś w posiadaniu tokenów xHDX, które kupiłeś podczas wydarzenia Balancer LBP?  Musisz najpierw [odebrać swoje HDX](/claim) zanim przejdziesz dalej.

:::

Po sprawdzeniu, że widzisz swoje saldo HDX, możesz przejść do interfejsu użytkownika stakowanie:

*Network* > *Staking*

Interfejs użytkownika składa się z następujących zakładek menu:

* **Staking overview**: tutaj znajdziesz listę wszystkich aktywnych walidatorów oraz kilka podstawowych informacji o każdym z nich, takich jak kwota HDX postawiona na nodzie, kwota własnej stawki walidatora oraz jak wysoka jest prowizja od nagrody. Ponadto, możesz zobaczyć liczbę punktów erowych zdobytych przez każdego walidatora w bieżącej erze oraz numer ostatniego bloku wyprodukowanego przez walidatora.
* **Działania na koncie**: tutaj możesz wnosić stawki i nominować.
* **Wypłaty**: tutaj możesz odebrać swoje nagrody za staking.
* **Cele**: tutaj możesz oszacować swoje zarobki. Jest to dobre miejsce na początek, gdy wybierasz węzeł walidatora do nominacji.
* **Oczekiwanie**: tutaj znajdziesz kolejkę oczekujących, w której umieszczane są nieaktywne walidatory, zanim zostaną włączone do zestawu aktywnych walidatorów. Walidator pozostanie w kolejce oczekujących dopóki nie otrzyma wystarczającej ilości staked HDX aby wejść do aktywnego zestawu walidatorów.
* **Statystyki walidatora**: tutaj możesz sprawdzić adres stash walidatora, aby zobaczyć szczegółowe informacje historyczne o zdobytych punktach era, wybranej stawce, nagrodach i ukośnikach. Gorąco zalecamy zapoznanie się z tymi informacjami przed powierzeniem walidatorowi swojej nominacji.

## 01 Zablokuj tokeny HDX {#01-bond-hdx-tokens}

:::warning

Bonded HDX tokens są stawką za zagwarantowanie bezpieczeństwa sieci. Niewłaściwe zachowanie nominowanego przez Ciebie węzła walidatora może zostać ukarane przez slashing, co może doprowadzić do nieumyślnej utraty Twoich środków. Zdecydowanie zalecamy, abyś dołożył należytej staranności przy wyborze walidatora, którego chcesz nominować.

:::

Aby połączyć tokeny HDX, przejdź do zakładki Account actions w interfejsie użytkownika Staking UI:

*Network* > *Staking* > *Account actions* > *+ Stash*

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/bond-hdx-1.png')} />
</div>

Po kliknięciu przycisku Stash powinny pojawić się preferencje wiązania z czterema edytowalnymi polami:
* **konto stash**: konto, na którym znajduje się większość Twoich tokenów HDX. HDX będzie stakowany z tego konta.
* **rachunek kontrolny**: rachunek przechowujący mniejszą część HDX potrzebną do pokrycia opłat związanych z rozpoczęciem i zakończeniem procesu nominacji.
* **wartość połączona**: ilość HDX, która jest połączona. Nie należy zabezpieczać wszystkich HDX, które się posiada - zamiast tego należy pozostawić część na pokrycie późniejszych opłat transakcyjnych.
* **miejsce docelowe płatności**: konto, na które zostaną wysłane nagrody za staking.


:::warning

Nie łącz wszystkich dostępnych tokenów HDX. Pozostaw niewielką rezerwę na pokrycie opłat transakcyjnych. Jeśli połączysz wszystkie tokeny HDX, które posiadasz, możesz nie być w stanie podpisać transakcji rozpoczynającej proces nominacji.

:::

Po ustawieniu preferencji Bonding, kliknij **Bond** i podpisz transakcję, aby zakończyć proces bondingu.

:::caution

Ze względów bezpieczeństwa nie jest zalecane posiadanie tych samych kont Stash i Controller. Jednakże, ponieważ transfery są wyłączone w Snakenet, nie jest obecnie możliwe korzystanie z oddzielnych kont. Gorąco zalecamy przejście na oddzielne konta Stash i Controller, jak tylko stanie się to możliwe w przyszłości.

:::

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/bond-hdx-2.png')} />
</div>

## 02 Nominuj walidatora {#02-nominate-a-validator}

Po sklejeniu HDX, można teraz nominować walidatora. Zanim to zrobisz, powinieneś zrobić wszystko, co w Twojej mocy i zdecydować, którego walidatora chciałbyś nominować na podstawie jego (dotychczasowych) wyników. Aby to zrobić, zapoznaj się z informacjami zawartymi w Staking UI, [omówionymi powyżej](#00-staking-ui).

:::note

HydraDX Snakenet ma **limit 64 nominatorów na jeden nod**. Wybierając noda do nominacji upewnij się, że validator nie osiągnął maksymalnej liczby nominacji, w przeciwnym razie Twoja nominacja będzie nieważna i nie otrzymasz nagrody za swoją stawkę. Liczbę nominacji dla każdego validatora można znaleźć w zakładce menu Oczekiwanie w interfejsie użytkownika Stakingu.

:::

Aby nominować jednego lub więcej walidatorów, przejdź do:

*Network* > *Staking* > *Account actions* > *Nominate* (przycisk obok Twojego połączonego HDX)

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-1.png')} />
</div>

Po kliknięciu na przycisk Nominuj powinieneś zobaczyć okienko o nazwie Nominuj walidatorów. W tym miejscu możesz wybrać jeden lub więcej walidatorów do nominowania z listy dostępnych walidatorów. Bardzo zalecane jest nominowanie wielu walidatorów, aby uniknąć sytuacji, w której nie będziesz aktywny, jeśli nie dostaniesz miejsca w jednym walidatorze (np. walidator jest przepełniony lub nie został wybrany do zestawu aktywnych walidatorów). Możesz nominować do 16 walidatorów. W każdej epoce tylko jedna z Twoich nominacji może być aktywna, nie możesz być wybrany przez kilku validatorów jednocześnie. Twoja stawka zostanie automatycznie przypisana do jednego z wybranych przez Ciebie walidatorów w taki sposób, aby zmaksymalizować decentralizację i zyski. Wybierasz tylko kwotę obligacji HDX i validatorów, którym ufasz.

Aby nominować wybranych walidatorów, kliknij Nominuj i podpisz transakcję.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-2.png')} />
</div>


## 03 Sprawdź status swoich nominacji  {#03-check-the-status-of-your-nominations}

Po zakończeniu procesu nominowania, Twoje nominacje będą nieaktywne przez resztę bieżącej ery. Po rozpoczęciu następnej ery, Twoje nominacje staną się aktywne, pod warunkiem, że przynajmniej jeden z nodów walidatorów, które nominowałeś, jest zawarty w aktywnym zestawie walidatorów i nie jest przepełniony, pomijając Ciebie. Jeśli wszystkie Twoje węzły walidacji pozostaną w kolejce oczekujących, Twoje nominacje również pozostaną nieaktywne i nie otrzymasz żadnych nagród za tę erę.

Aby sprawdzić status swoich nominacji, przejdź do:

*Network* > *Staking* > *Account actions*

Możesz zobaczyć swoje nieaktywne nominacje w sekcji *Waiting nominations*:

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-3.png')} />
</div>

Gdy nominacja stanie się aktywna, powinieneś znaleźć ją na liście *Active nominations*

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-4.png')} />
</div>  

:::note

Upewnij się, że raz na jakiś czas sprawdzisz swoje nominacje. Jest możliwe, że niektóre z Twoich walidatorów zmienią swój procent prowizji, co będzie miało negatywny wpływ na Twoje nagrody. Sprawdzając często status swoich nominacji będziesz mógł zareagować aktualizując listę swoich nominowanych walidatorów.

:::

## 04 Dostosuj swoje nominacje

Jeśli niektóre z Twoich walidatorów są przepełnione lub zmieniły swoją prowizję, możesz chcieć dostosować swoje nominacje.

Aby to zrobić, otwórz Polkadot/apps i przejdź do:  
*Network* > *Staking* > *Account actions*

Kliknij na trzy kropki obok szczegółów Twojego konta i wybierz opcję _Set nominees_.

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-set-nominees.png')} />
</div>

W poniższym oknie, które może wydawać się znajome, możesz usunąć walidatory i/lub dodać nowe.  
Zmiana nominacji może być dokonywana na bieżąco, nie ma potrzeby przerywania nominacji. Zmiany zostaną zastosowane, gdy rozpocznie się następna era (24h).

<div style={{textAlign: 'center'}}>
  <img src={useBaseUrl('/nominator-guide/nominate-validator-2.png')} />
</div>  

Dziękujemy za wsparcie HydraDX poprzez nominowanie Snakenet! 🎉
