---
id: staking
title: Staking
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Ta sekcja zawiera krótkie wprowadzenie do tego, jak działa stakowanie w sieci HydraDX. Jeśli nie jesteś zaznajomiony z stakowaniem w sieci opartej na substrate, zalecamy przeczytanie tego artykułu przed podjęciem decyzji o uczestnictwie.

Mechanizm konsensusu używany przez HydraDX nazywa się Nominated Proof-of-Stake (NPoS). NPoS jest odmianą Proof-of-Stake i jest używany w blockchainach opartych na substracie, takich jak Polkadot i Kusama. Dwie główne role w środowisku NPoS nazywają się [**Walidatorami**](#validators) oraz [**nominatorami**](#nominators). 

### Walidatorzy {#validators}

Walidatorzy uczestniczą w sieci poprzez uruchamianie tzw. węzłów walidacyjnych (ang. validator nodes), które zapewniają infrastrukturę umożliwiającą bezpieczne działanie sieci HydraDX. Węzły walidacyjne spełniają trzy funkcje, które są niezwykle ważne do poprawnego działania mechanizmu konsensusu. W pierwszej kolejności weryfikują i zatwierdzają one informacje zawarte w blokach, takie jak tożsamość uczestników i przedmiot transakcji. Po drugie, walidatorzy uczestniczą w tworzeniu nowych bloków w oparciu o deklaracje ważności innych walidatorów. Po trzecie, gwarantują one ostateczność transakcji blockchain, czyli to, że dana transakcja dojdzie do skutku.

Ważną cechą NPoS jest to, że nie wszyscy walidatorzy uczestniczą w procesie potwierdzania transakcji w tym samym czasie. Tylko walidatorzy, którzy znajdują się w aktywnym zestawie walidatorów wykonują wyżej wymienione operacje i otrzymują za to [nagrody](/staking_rewards). Zestaw aktywnych walidatorów jest ograniczony do ustalonej liczby węzłów (ang. nodes). W [HydraDX Snakenet](/snakenet) spodziewamy się, że liczba ta będzie wynosić około 300 i będzie wzrastać w miarę postępów w kierunku mainnetu.

Ważną cechą NPoS jest to, że nie wszyscy walidatorzy uczestniczą w procesie potwierdzania transakcji w tym samym czasie. Tylko walidatorzy, którzy znajdują się w aktywnym zestawie walidatorów wykonują wyżej wymienione operacje i otrzymują za to nagrody. Zestaw aktywnych walidatorów jest ograniczony do ustalonej liczby węzłów (ang. nodes). W HydraDX Snakenet spodziewamy się, że liczba ta będzie wynosić około 300 i będzie wzrastać w miarę postępów w kierunku mainnetu. Walidatorzy są wybierani do aktywnego zestawu zgodnie z zasadą proporcjonalnej, uzasadnionej reprezentacji. Zasada ta ma na celu ochronę decentralizacji i sprawiedliwej reprezentacji poprzez przydzielanie dostępnych miejsc walidatorom proporcjonalnie do ich nominowanego udziału. Im większa liczba „zastakowanych” tokenów u danego walidatora, tym większa szansa, że jego węzeł zostanie wybrany do aktywnego zestawu. Walidatorzy, którzy nie znajdą się w aktywnym zestawie, są umieszczani na liście oczekujących. Zestaw aktywnych walidatorów jest aktualizowany na początku każdej ery (24h), zapewniając ewentualne okno wejściowe dla nowych walidatorów.

:::note

W sieci opartej na substrate czas jest podzielony na jednostki zwane **erami**. W [HydraDX Snakenet](/snakenet), *1 Era = 24 godziny*.

:::

Uczestnictwo w charakterze walidatora wymaga pewnego poziomu wiedzy technicznej w zakresie bezpiecznego zakładania oraz utrzymywania węzła walidatora. Nieprawidłowe działanie węzła walidatora może zostać ukarane (ang. slashing), co może skutkować mimowolną utratą Twoich środków oraz Twoich nominatorów. Jeśli uważasz, że masz doświadczenie niezbędne do założenia oraz prowadzenia węzła walidatora, możesz zapoznać się z naszym [przewodnikiem zostać validatorem](/node_setup). W przeciwnym razie zdecydowanie zalecamy rozważenie udziału w roli nominatora.

### Nominatorzy {#nominators}

Nominatorzy pomagają zabezpieczyć sieć, wyznaczając walidatorów, którzy mają zostać wybrani do aktywnego zestawu walidatorów. Robią to, stakują swoje tokeny HDX u wybranych przez siebie walidatorów. Proces nominacji nie wymaga uruchamiania oraz utrzymywania węzłów, dzięki czemu ta forma stakowania jest dostępna dla wszystkich, nawet tych bez technicznej wiedzy. Tokeny używane do wyznaczania walidatorów są zablokowane, co oznacza, że są zamrożone i nie można ich używać do innych celów. W każdej chwili można zmienić walidatora lub zatrzymać swoje nominacje, a zmiany te zostaną zaktualizowane pod koniec bieżącej ery (24h). Nominatorzy mogą również odblokować swoje tokeny (te które zostały zamrożone w chwili wyznaczania walidatora), jednak stanie się to skuteczne dopiero po upływie okresu oczekiwania wynoszącego *28 dni* po dokonaniu transakcji odblokowywania.

Przed nominacją zawsze należy dołożyć należytej staranności i sprawdzić wiarygodność wybranych walidatorów. Możesz to zrobić poprzez sprawdzenie ich tożsamości, jak również informacji historycznych, takich jak punkty ery, wybrana stawka, nagrody oraz kary (slashes). Jednak na początku istnienia Snakenetu znalezienie wszystkich tych informacji może być trudne. Jeśli masz wątpliwości co do wyboru walidatorów, skontaktuj się z nami na Discordzie, a udostępnimy Ci listę zaufanych walidatorów przygotowaną przez naszą społeczność.

Kolejną kwestią do rozważenia przy wyborze walidatora jest *procent prowizji od nagrody*. Stanowi to część nagród, które zostaną wypłacone walidatorowi za świadczenie usług na rzecz nominatorów. Najniższy procent prowizji nie zawsze jest najlepszy - prowadzenie wydajnego i dostępnego węzła (noda) wiąże się z wysokimi kosztami operacyjnymi, które można w sposób zrównoważony pokryć jedynie poprzez żądanie realistycznej prowizji.

W HydraDX można wyznaczyć  **maximum of 16 validators** Wyznaczenie więcej niż jednego walidatora nie musi jednak oznaczać, że tokeny które stajkujesz zostaną za każdym razem przypisana do wszystkich wybranych walidatorów. Kiedy rozpocznie się kolejna era, Substrate uruchomi serię złożonych algorytmów, w celu określenia najbardziej optymalnej dystrybucji wszystkich nominacji w sieci, a ostatecznym celem będzie podjęcie decyzji, którzy walidatorzy mają być włączeni do zestawu aktywnych walidatorów. Jeśli żaden z wybranych walidatorów nie otrzyma wystarczającego wsparcia, aby dołączyć do aktywnego zestawu, Twoje **nominację pozostaną nieaktywne** nieaktywne przez czas trwania ery (24 godziny), za ten okres nie otrzymasz również żadnych nagród. Aby zmaksymalizować szanse włączenia Twojego udziału do zestawu aktywnych walidatorów, zdecydowanie zalecamy **nominowanie kilku walidatorów**, co również przyczyni się do naszych wysiłków na rzecz wzmocnienia decentralizacji

:::note

Upewnij się, że nie wyznaczasz walidatorów, których liczba nominatorów jest przekroczona. Obecnie istnieje **limit 64 nominacji dla jednego walidatora**, po przekroczeniu, którego następuje tzw. „nadsubskrypcja”. Kiedy rozpocznie się następna era, walidator z nadsubskrypcją zostanie wybrany tylko wraz z maksymalną dozwoloną liczbą nominatorów (64). W takim przypadku pierwszeństwo mają nominatorzy z najwyższym udziałem, podczas gdy nominatorzy z najniższym udziałem zostaną zignorowani i nie otrzymają żadnych nagród w tej erze. Nominowanie jest bardziej przystępną formą obstawiania, ale wiąże się również z ryzykiem. Walidatorzy łamiący zasady sieci mogą zostać ukarani slashem, co skutkuje utratą środków zarówno po stronie walidatora, jak i jego nominatorów. Dlatego ważne jest, aby wyznaczyć tylko węzły (nody) o uznanej reputacji.

Nominowanie jest bardziej przystępną metodą stakingu ale wiąże się z ryzykiem. Walidatorzy kótrzy naruszją zasady panujące w sieci, będą karani przez slashing, co w rezultacie może spowodować utratę środków nominatora oraz walidatora. Dlatego, bardzo ważne jest nominowanie jedynie zaufanych walidatorów.

:::

Czy jesteś zainteresowany stakowaniem swoich tokenów HDX poprzez nominowanie walidatorów? Sprawdź nasz [przewodnik nominatora](/start_nominating) aby rozpocząć nominację!
