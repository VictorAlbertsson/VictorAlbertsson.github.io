---
title: "Funktionell Programmering"
author:
  - Victor Albertsson
---

# Funktionell Programmering

---

# Problem med imperativ programmering

- Skapar svårfångade buggar
- Svårt att optimera
   - Samtidighet
   - Parallelism
- Problem med minnessäkerhet

---

# Grundläggande principer

---

## Oföränderlighet

- Variabler och funktioner kan endast initieras
  - Inga loopar
  - Inga arrays
  - Inga configurationsvariabler

---

## Funktioner hela vägen ner

- Program ska delas in i många små funktioner
- Funktioner konstrueras från mindre funktioner utan att deras betydelse ändras

---

```scheme
#lang scheme
(require scheme/function)
((curry + 10) 20) ; = (+ 10 20)
;; 30

(map (curry + 10) (list 20 40 60))
;; '(30 50 70)

((compose sqrt +) 16 9)
;; 5
```

---

## Induktiva typer

- Rekursiva funktioner blir ett naturlig verktyg
- Även ‘pattern matching’ blir möjligt

```scheme
#lang typed/scheme
(define-type (List A) 
             (Rec List (Pair A (U List Null))))
;; ‘Rec’ skapar en anonym datatyp
```

---

# Konsekvenser

---

## Matematiska resonemang

- *"If it is to be effective as a tool of thought, a notation must allow convenient expression not only of notions arising directly from a problem, but also of those arising in subsequent analysis, generalization, and specialization."* -- Kenneth E. Iverson
- Typer som propositioner och funktioner av typer som bevis
- Verifiering av kodsäkerhet blir möjligt

---

## Starkare optimering

- Samtidighet (Erlang)
- Parallelism (APL)

---

## Modularitet

- Eliminering av kopplingar mellan orelaterad kod
- Alla värden som en funktion kan anta måste vara väldefinierade

---

## Rekursion

- Kan skapa eleganta lösningar
- Kräver mer kognitiv ansträngning i tidskritiska applikationer
- Effektiv rekursion kräver att språket stödjer vissa optimeringsstrategier (tail-call elimination)

---

# Deklarativ programmering

- *VAD* som ska göras utan *HUR* det ska utföras

---

## Prolog 

[The Power of Prolog](https://www.youtube.com/channel/UCFFeNyzCEQDS4KCecugmotg)

```prolog
:- use_module(library(reif)).

list_without([], _, []).
list_without([X|Xs], E, Ys) :-
    if_(X=E, Ys=Ls, Ys=[X|Ls]),
    list_without(Xs, E, Ls).
```

---

## Den deklarativa hierarkin

| Endast reversibla funktioner | Monoton                           |
| Inga mutationer              | Icke-monoton, Rent funktionell    |
| Begränsade mutationer        | Monadisk, Substrukturell et al    |
| Obegränsade mutationer       | Imperativ                         |

---

# Fin
