# CANDU-6 – model pełnego rdzenia 3D w Serpent 2

Projekt na przedmiot *Metody numeryczne* (AGH).

## Pliki wejściowe

| plik | zawartość |
|---|---|
| `Candu.txt` | plik główny: `include`, parametry obliczeń, wykresy, detektory |
| `materials.txt` | materiały (paliwo UO2, Zircaloy, D2O…) i dane S(α,β) |
| `fuelrod.txt` | pręt paliwowy na całą długość kanału (12 wiązek) – uniwersum `F` |
| `channel.txt` | wiązka 37-prętowa (`BUN`) i kanał paliwowy (`CH`) |
| `core.txt` | siatka 380 kanałów (`CORE`) i kalandria (uniwersum `0`) |

## Uruchomienie

```
sss2 -plot Candu.txt      # tylko wykresy geometrii
sss2 -omp 8 Candu.txt     # pełne obliczenia
```

Pliki muszą mieć końce linii LF (wymuszone przez `.gitattributes`).

## Źródła

Dane geometryczne i materiałowe na podstawie: *Burnup Calculation of a CANDU6 Reactor Using the Serpent and MCNP6 Codes* oraz *Feasibility Study for Minor Actinides Transmutation in Conventional Power Reactors*.
