# MineProgress 0.7.0 — Paper 1.21.11

MineProgress 0.7.0 dodaje system rozwoju specjalnego kilofa i jego prestiżu. To **projekt źródłowy**: gotowy JAR powstaje po poprawnej kompilacji w GitHub Actions. Ta paczka nie zawiera potwierdzonego, przetestowanego JAR-a.

## Nowy system kilofa
- Gracz otrzymuje specjalny **drewniany kilof MineProgress na poziomie 0**. Przy pierwszym wejściu plugin daje go, jeśli gracz nie ma już specjalnego kilofa w ekwipunku.
- Kilof zdobywa XP za bloki wykopane w skonfigurowanych kopalniach.
- Domyślna progresja ma 20 poziomów na materiał:
  - 0–3: Efektywność I
  - 4–7: Efektywność II
  - 8–11: Efektywność III + Fortuna I
  - 12–15: Efektywność IV + Fortuna II
  - 16–20: Efektywność V + Fortuna III
- Na poziomie 20 (domyślnie, konfigurowalne) gracz wybiera ulepszenie w GUI lub wpisuje `/kilof ulepsz`. Kilof przechodzi kolejno na kamienny, żelazny, złoty, diamentowy i netherytowy, a jego poziom oraz XP wracają do 0.
- Wymagane XP kilofa rośnie z każdym poziomem zgodnie ze wzorem baza + poziom × przyrost. Domyślnie poziom 0 wymaga 10 XP, poziom 1 wymaga 12 XP itd. Progi i poziomy enchantów są konfigurowalne w `pickaxe-progression`. Każde ulepszenie materiału zwiększa prestiż kilofa o 1. Po osiągnięciu skonfigurowanego poziomu maksymalnego na netherytowym kilofie, prestiż resetuje go do drewnianego i zwiększa licznik prestiżu. Każdy prestiż kilofa daje domyślnie +1% zarobków z kopania.
- Dane progresji przechowywane są w `plugins/MineProgress/players.yml`. Nie usuwaj tego pliku podczas aktualizacji.

## Dodatkowe systemy
### Szczęśliwa żyła
Przy kopaniu rud Fortuna ma dodatkową szansę na bonusowy drop oprócz standardowych dropów Minecrafta:
- Fortuna I: 8% szansy
- Fortuna II: 16% szansy
- Fortuna III: 24% szansy
- Jeśli efekt zadziała, wypada 1 dodatkowy surowiec, z dodatkową szansą 25% na drugi.

Działa dla węgla, miedzi, żelaza, złota, diamentów, szmaragdów, lapisu, redstone, złota z Netheru i kwarcu. Szansa jest konfigurowalna w `config.yml`.

### Seria wydobycia
Jeśli gracz kopie kolejne bloki w kopalni bez przerwy dłuższej niż 10 sekund, buduje serię. Co 10 bloków otrzymuje +2% zarobków, maksymalnie +20%. Seria jest chwilowa i nie jest zapisywana po wyjściu.

## GUI i komendy gracza
- `/mineprogress` lub `/mp` — główne menu
- `/kilof` — GUI kilofa: poziom, XP, materiał, enchanty, prestiż, Szczęśliwa Żyła, Seria Wydobycia, ulepszenie i przycisk „Odbierz nowy kilof”
- `/kilof ulepsz` — wykonaj ulepszenie, gdy kilof osiągnie maksymalny poziom ustawiony w config.yml
- `/lopata` — GUI rozwoju łopaty MineProgress; kliknij skrzynię, aby otrzymać aktualną łopatę
- `/siekiera` — GUI rozwoju siekiery MineProgress; kliknij skrzynię, aby otrzymać aktualną siekierę
- `/kopalnia` — statystyki kopania
- `/prestiz` i `/prestiz confirm` — prestiż gracza. Ten system resetuje poziom gracza, ale **nie resetuje już osobnego postępu kilofa**.

## Komendy administracyjne
- `/mineadmin gui` — panel administracyjny
- `/mineadmin wand` — drewniana motyka MineProgress do zaznaczenia regionu
- Lewy klik blokiem: punkt 1; prawy klik: punkt 2
- `/mineadmin create <nazwa> [region|blocks]` — utwórz kopalnię
- `/mineadmin blocks <nazwa> <STONE,COAL_ORE>` — dozwolone materiały w trybie `blocks`
- `/mineadmin set <nazwa> <pieniądze> <xpGracza> <xpKilofa> <sekundy>` — ustaw nagrody i regenerację
- `/mineadmin givepickaxe <gracz>` — wydaj specjalny kilof
- `/mineadmin placeholders` — lista placeholderów
- `/mineadmin list` — lista kopalń
- `/mineadmin delete <nazwa>` — usuń kopalnię, jej hologram i plik snapshotu
- `/mineadmin restart <nazwa>` — natychmiast odtwórz zapisany stan kopalni
- `/mineadmin particles <nazwa> <on|off>` — włącz/wyłącz particle na krawędziach regionu
- `/mineadmin tool <nazwa> <PICKAXE|STONE_PICKAXE|SHOVEL|AXE>` — ustaw wymagany typ narzędzia; można wskazać też dokładny materiał, np. `STONE_PICKAXE`
- `/mineadmin hologram <nazwa> <1-3> <tekst>` — zmień wybraną linię hologramu; dostępne placeholdery: `{name}`, `{blocks}`, `{regen}`, `{tool}`, `{world}`
- `/mineadmin xp <gracz> <player|pickaxe|shovel|axe> <ilość>` — dodaj XP do wybranej ścieżki
- `/mineadmin level <gracz> <player|pickaxe|shovel|axe> <poziom>` — ustaw poziom wybranej ścieżki
- `/mineadmin reload` — wczytaj config i kopalnie ponownie
- Komendy podpowiadają dostępne podkomendy, nazwy kopalń, graczy online i materiały.

## Granice i hologramy
- Dla każdej kopalni tworzony jest hologram z nazwą, blokami i odliczaniem regeneracji. Linie są zapisywane dla każdej kopalni w `mines.yml`; edycja komendą `/mineadmin hologram`.
- Particle na krawędziach regionu są domyślnie wyłączone. Włącz je osobno dla kopalni komendą `/mineadmin particles <nazwa> on`.
- Specjalny kilof MineProgress ma niezniszczalność włączoną w metadanych; jego trwałość nie spada.

## Nowe placeholdery PlaceholderAPI
- `%mineprogress_pickaxe_material%` — materiał kilofa (np. Kamienny)
- `%mineprogress_pickaxe_tier%` — numer materiału (0–5)
- `%mineprogress_pickaxe_prestige%` — prestiż kilofa
- `%mineprogress_pickaxe_efficiency%` — aktualny poziom Efektywności
- `%mineprogress_pickaxe_fortune%` — aktualny poziom Fortuny
- Dotychczasowe placeholdery postępu gracza, XP, kilofa, zarobków, rankingów i regeneracji pozostają dostępne.

## Konfiguracja systemów narzędzi
Wymagania XP i maksymalne poziomy kilofa, łopaty i siekiery konfiguruje się niezależnie:
```yaml
settings:
  max-pickaxe-level: 20
  pickaxe-xp-base: 10
  pickaxe-xp-increase-per-level: 2
  max-shovel-level: 5
  shovel-xp-base: 25
  shovel-xp-increase-per-level: 10
  max-axe-level: 5
  axe-xp-base: 25
  axe-xp-increase-per-level: 10
  pickaxe-prestige-money-bonus: 0.01
pickaxe-progression:
  efficiency-1: 1
  efficiency-2: 2
  efficiency-2-level: 4
  efficiency-3: 3
  efficiency-3-level: 8
  efficiency-4: 4
  efficiency-4-level: 12
  efficiency-5: 5
  efficiency-5-level: 16
  fortune-1: 1
  fortune-1-level: 8
  fortune-2: 2
  fortune-2-level: 12
  fortune-3: 3
  fortune-3-level: 16
fortune:
  bonus-chance-per-level: 0.08
  double-drop-chance: 0.25
mining-streak:
  timeout-seconds: 10
  blocks-per-step: 10
  money-bonus-per-step: 0.02
  max-bonus: 0.20
```

## Wymagania
- Paper 1.21.11
- Java 21
- Vault i plugin ekonomii dla wypłat
- PlaceholderAPI dla placeholderów

## Budowanie przez GitHub Actions
1. Wgraj całą zawartość katalogu projektu do repozytorium GitHub, łącznie z ukrytym katalogiem `.github`.
2. Wejdź w **Actions** i uruchom **Build MineProgress**.
3. Po zielonym wyniku pobierz artefakt `MineProgress-0.7.0`.
4. Przed podmianą zrób kopię JAR-a oraz folderu `plugins/MineProgress`.
5. Testuj na kopii serwera. Jeśli kompilacja lub uruchomienie zgłosi błąd, zapisz pełny log.


## MineProgress 0.7.0 — poprawki progresji
- Prestiż kilofa nalicza się tylko raz po pełnym obiegu: drewno → kamień → żelazo → złoto → diament → netheryt → drewno.
- Jednorazowa migracja przelicza dotychczasowe prestiże materiałowe (dzielenie przez 6).
- Reset kilofa wymaga komendy `/kilof reset`, a następnie `/kilof reset confirm` w ciągu 30 sekund.
- Specjalny kilof jest deduplikowany w ekwipunku przy wejściu; wydanie odświeżonego kilofa zastępuje poprzedni egzemplarz w ekwipunku.
- Uproszczono premie serii, dropu i prestiżu; parametry są w config.yml.
- Poziom gracza daje konfigurowalny bonus do monet, a prestiż gracza resetuje poziom do 1 i daje osobny stały bonus.
- GUI progresji gracza pokazuje XP, bonus poziomów i działanie prestiżu.


## Wydanie 0.7.1
Poprawiono błąd kompilacji: dodano deklarację mapy czasowych potwierdzeń resetu kilofa (`pendingPickaxeReset`), używanej przez komendę `/kilof reset confirm`.
