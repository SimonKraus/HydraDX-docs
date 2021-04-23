---
id: staking_rewards
title: Staking Rewards
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Nagrody za stakowanie motywują walidatorów i nominatorów do [stakowania swoich tokenów HDX](/staking). Istnieją trzy rodzaje nagród za stakowanie, które są omawiane w tym artykule: [nagrody podstawowe](#base-rewards), [punkty za erę](#era-points) oraz [napiwki](#tips).

## Nagrody podstawowe {#base-rewards}

Na koniec każdej ery (która trwa 24 godziny) wszystkie aktywne pool-e walidatorów otrzymują podstawowe nagrody w postaci tokenów HDX. Pool-a walidatorów składa się z wybranego walidatora (posiadającego zestakowane swoje własne tokeny HDX) i wszystkich aktywnych nominacji, które wspierają walidatora (więcej informacji znajduje się w sekcji [stakowania](/staking)). Główną zasadą mechanizmu konsensusu Nominated Proof of Stake (NPoS) jest to **że ta sama praca przynosi takie same nagrody**. Innymi słowy, ponieważ wszystkie pool-e walidatorów zasadniczo wykonują tę samą pracę, **dostępne nagrody podstawowe są dzielone po równo**. Oznacza to, że pool-e walidatorów **nie** są wynagradzane proporcjonalnie do ilości zestakowanych tokenów w pool-u, co jest główną różnicą w porównaniu z tradycyjnymi sieciami Proof of Stake.

Mechanizm równego podziału nagród podstawowych między wszystkie uczestniczące pool-e walidatorów przyczynia się do bezpieczeństwa sieci, zapobiegając koncentracji władzy w kilku pool-ach walidatorów, wzmacniając w ten sposób decentralizację. Z biegiem czasu zachęca to nominatorów do nominowania walidatorów z mniejszą ilością zestkowanych tokenów HDX. Ten proces ostatecznie zrównoważy relacje władzy w sieci i doprowadzi do sytuacji, w której wszystkie pool-e walidatorów mają mniej więcej taką samą liczbę zestakowanych tokenów HDX.

Dystrybucja nagród przebiega w następujący sposób. Po wyliczeniu (równej) kwoty nagród dla każdej pool-i walidatorów, walidator otrzymuje swój udział w postaci **prowizji** za utrzymanie węzła. W drugim etapie pozostałe tokeny są rozdzielane **proporcjonalnie** między wszystkich nominatorów (w tym dla walidatora, który sam stakuje swoje tokeny HDX). Oznacza to, że nominatorzy z większą ilością zestakowanych tokenów HDX w danycm pool-u otrzymają większą część nagród przypisanych do tego pool-a.

:::note
W testnecie zachęt (incentivized testnet) o nazwie Snakenet, APY nagród za stakowanie tokenów HDX jest szacowane na około **50% APY**.
:::

## Punkty za erę {#era-points}

Walidatorzy mogą zdobyć dodatkowe nagrody proporcjonalnie do punktów ery, które zdobyli w minionej erze. Te nagrody są dodawane do nagród podstawowych opisanych powyżej. Weryfikatorzy mogą zdobywać punkty ery, wykonując określone czynności, takie jak:

* tworzenie bloku non-uncle na Relay Chain.
* tworzenie odniesienia do bloku uncle, do którego wcześniej nie było odniesień.
* tworzenie bloku uncle, do którego się odwołuje.

:::note
Blok uncle to blok Relay Chain, ważny pod każdym względem, który jednak nie stał się kanoniczny. Może się tak zdarzyć, gdy dwoje lub więcej walidatorów są producentami bloków w jednym slocie i blok wyprodukowany przez jednego walidatora dociera do następnego producenta bloku przed innymi. Bloki spóźnione nazywane są blokami uncle.
:::

## Napiwki {#tips}

Ostatecznie, walidatorzy mogą zdobywać napiwki, które są również dodawane do podstawowych nagród na koniec każdej ery. Napiwki stanowią dodatkową opłatę transakcyjną, którą użytkownicy mogą opcjonalnie uiścić, aby nadać transakcjom wyższy priorytet.
