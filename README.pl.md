# CANDU-6 – model pełnego rdzenia 3D w Serpent 2

*[English version](README.md)*

Projekt na przedmiot *Metody numeryczne* (AGH): model Monte Carlo pełnego rdzenia
CANDU-6 (380 kanałów paliwowych, 37-prętowe wiązki z uranem naturalnym, moderator
i reflektor z ciężkiej wody) w kodzie Serpent 2.

## Pliki wejściowe

Model składa się z zagnieżdżonych uniwersów, od najmniejszego do największego:

| plik | zawartość | uniwersum |
|---|---|---|
| `materials` | paliwo UO2, Zircaloy-4, Zr-2.5%Nb, Zircaloy-2, gaz w szczelinie, D2O: chłodziwo / moderator / reflektor, dane S(α,β) | – |
| `fuelrod` | pręt paliwowy na całą długość kanału (12 wiązek × 49.53 cm) | `F` |
| `channel` | wiązka 37-prętowa (siatka kołowa) i kanał: rura ciśnieniowa, szczelina gazowa, rura kalandrii, moderator | `BUN`, `CH` |
| `core` | siatka kwadratowa 380 kanałów (podziałka 28.575 cm) w kalandrii (R = 379.7 cm) | `CORE`, `0` |
| `CANDU` | plik główny: `include`, parametry obliczeń, wykresy, detektory | – |

## Uruchomienie

```
serpent -plot CANDU       # tylko wykresy geometrii
serpent CANDU             # pełne obliczenia
serpent -omp 8 CANDU      # równolegle, 8 wątków
```

Główne wyniki: `CANDU_res.m` (k-eff: `ANA_KEFF`, `IMP_KEFF`),
detektory w `CANDU_det0.m` – mapa mocy kanałowej (`ChPower`), moc osiowa na wiązkę
(`AxPower`), strumień dwugrupowy wzdłuż średnicy rdzenia (`FluxX`).

## Założenia modelu

- świeże paliwo z uranu naturalnego, jedna temperatura paliwa (1200 K),
- brak urządzeń sterujących (adjustery, absorbery),
- bez płyt końcowych wiązek i osłon czołowych; poza kalandrią próżnia,
- dane jądrowe: JEFF-3.2 (przekroje czynne), JEFF-3.1 (rozpraszanie termiczne).

## Źródła

Dane geometryczne i materiałowe na podstawie:

- *Burnup Calculation of a CANDU6 Reactor Using the Serpent and MCNP6 Codes*
- *Feasibility Study for Minor Actinides Transmutation in Conventional Power Reactors*
- Serpent Wiki – *2D CANDU fuel bundle geometry*
