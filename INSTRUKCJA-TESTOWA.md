# MineProgress 0.7.0 — lista testów

## Przed aktualizacją
- [ ] Zatrzymaj serwer i skopiuj cały folder `plugins/MineProgress`.
- [ ] Zachowaj stary JAR, aby móc wrócić do poprzedniej wersji.
- [ ] Zbuduj JAR przez GitHub Actions; ta paczka to źródła, nie gotowy JAR.

## Start i kilof
- [ ] Uruchom Paper 1.21.11 z Java 21, Vault i pluginem ekonomii.
- [ ] Sprawdź, czy nowy gracz otrzymuje drewniany Kilof MineProgress na poziomie 0.
- [ ] Sprawdź, czy kilof ma Efektywność I.
- [ ] Wykop bloki w kopalni i sprawdź przyrost XP.
- [ ] Sprawdź domyślne progi: 4 = Efektywność II; 8 = Efektywność III + Fortuna I; 12 = Efektywność IV + Fortuna II; 16 = Efektywność V + Fortuna III.
- [ ] Na poziomie 20 (domyślnie) otwórz `/kilof`, kliknij ulepszenie i sprawdź, czy materiał przechodzi na kamienny, a poziom/XP wracają do 0.
- [ ] Powtórz ulepszanie do żelaza, złota, diamentu i netherytu.
- [ ] Na poziomie maksymalnym ustawionym w config.yml netherytowego kilofa sprawdź prestiż, reset do drewna i bonus zarobków.
- [ ] Wyjdź i wejdź ponownie; sprawdź zachowanie poziomu, materiału, enchantów i prestiżu.

## Bonusowe mechaniki
- [ ] Z Fortuną I/II/III kop rudę wielokrotnie i sprawdź wiadomość „Szczęśliwa żyła” oraz bonusowe dropy.
- [ ] Kop 10, 20, 30 itd. bloków bez przerwy i sprawdź serię oraz rosnący bonus monet do +20%.
- [ ] Zrób przerwę dłuższą niż 10 sekund i sprawdź, czy seria zaczyna się od nowa.
- [ ] Sprawdź `/kilof ulepsz` przed poziomem maksymalnym — powinien odmówić ulepszenia.

## GUI i integracje
- [ ] `/mineprogress` → kliknij ikonę kilofa.
- [ ] Sprawdź poziom, XP, materiał, enchanty, prestiż, opis Fortuny i Serii Wydobycia.
- [ ] Kliknij „Odbierz nowy kilof” i sprawdź, że dostajesz jeden aktualny kilof bez utraty progresu.
- [ ] Sprawdź `%mineprogress_pickaxe_material%`, `%mineprogress_pickaxe_prestige%`, `%mineprogress_pickaxe_efficiency%` i `%mineprogress_pickaxe_fortune%` w PlaceholderAPI.
- [ ] Sprawdź, czy `/prestiz confirm` resetuje poziom gracza, ale nie resetuje kilofa.
- [ ] Sprawdź log serwera po starcie oraz podczas kopania.

## Jeśli coś nie działa
Wyślij pełny błąd z konsoli, dokładny krok testu, wersję Paper, wersje Vault/ekonomii i PlaceholderAPI. Nie testuj pierwszej kompilacji na serwerze produkcyjnym.


## MineProgress 0.7.0 — nowe testy
- [ ] `/mineadmin delete <nazwa>` usuwa kopalnię z listy, `mines.yml`, snapshot i hologram.
- [ ] `/mineadmin restart <nazwa>` natychmiast odtwarza snapshot i anuluje zaplanowaną regenerację.
- [ ] `/mineadmin particles <nazwa> on` pokazuje krawędzie regionu, a `off` je wyłącza; ustawienie pozostaje po restarcie.
- [ ] Hologram wyświetla nazwę kopalni, informację o blokach i czas do regeneracji, a po regeneracji pokazuje „Gotowa”.
- [ ] Wpisywanie `/mineadmin`, `/mineadmin delete `, `/mineadmin particles <nazwa> ` oraz `/kilof ` pokazuje podpowiedzi.
- [ ] Specjalny kilof nie traci trwałości podczas kopania.
- [ ] Przeładowanie danych nie tworzy duplikatów hologramów.

- [ ] Sprawdź, czy XP wymagane na kolejny poziom rośnie zgodnie z `pickaxe-xp-base` i `pickaxe-xp-increase-per-level`.
- [ ] Zmień progi w `pickaxe-progression`, przeładuj serwer i sprawdź enchanty kilofa.
- [ ] W GUI `/kilof` kliknij „Odbierz nowy kilof” i potwierdź, że kilofy MineProgress w ekwipunku zostały zastąpione jednym odświeżonym egzemplarzem, bez utraty poziomu i prestiżu.


## Testy wersji 0.7.0
- [ ] `/mineadmin tool kopalnia2 STONE_PICKAXE` blokuje kopanie zwykłym kilofem i innymi materiałami; przepuszcza specjalny kamienny kilof MineProgress.
- [ ] `/mineadmin tool kopalnia2 SHOVEL` wymaga specjalnej łopaty MineProgress; analogicznie `AXE` dla siekiery.
- [ ] `/lopata` i `/siekiera` otwierają GUI; odbiór narzędzia nie resetuje postępu.
- [ ] XP łopaty i siekiery rośnie tylko podczas kopania w kopalni wymagającej odpowiedniego narzędzia.
- [ ] Przy maksymalnym poziomie można ulepszyć materiał łopaty/siekiery; poziom i XP resetują się, a narzędzie pozostaje niezniszczalne.
- [ ] `/mineadmin xp <gracz> shovel 100` oraz `/mineadmin level <gracz> axe 3` aktualizują statystyki i narzędzia.
- [ ] `/mineadmin hologram kopalnia2 1 &6Kopalnia: &e{name}` zapisuje linię po restarcie; sprawdzić `{blocks}`, `{regen}` i `{tool}`.
- [ ] Hologram nie duplikuje się po restarcie, `/mineadmin reload` ani edycji linii.


## MineProgress 0.7.0 — poprawki progresji
- Prestiż kilofa nalicza się tylko raz po pełnym obiegu: drewno → kamień → żelazo → złoto → diament → netheryt → drewno.
- Jednorazowa migracja przelicza dotychczasowe prestiże materiałowe (dzielenie przez 6).
- Reset kilofa wymaga komendy `/kilof reset`, a następnie `/kilof reset confirm` w ciągu 30 sekund.
- Specjalny kilof jest deduplikowany w ekwipunku przy wejściu; wydanie odświeżonego kilofa zastępuje poprzedni egzemplarz w ekwipunku.
- Uproszczono premie serii, dropu i prestiżu; parametry są w config.yml.
- Poziom gracza daje konfigurowalny bonus do monet, a prestiż gracza resetuje poziom do 1 i daje osobny stały bonus.
- GUI progresji gracza pokazuje XP, bonus poziomów i działanie prestiżu.

### Testy wersji 0.7.0
- [ ] Wykonaj pełny cykl materiałów kilofa (drewno → kamień → żelazo → złoto → diament → netheryt → drewno): prestiż powinien wzrosnąć dokładnie o 1.
- [ ] Zweryfikuj migrację istniejących danych: stary prestiż kilofa jest przeliczany na pełne obiegi, dzieląc wartość przez 6 (migracja jednorazowa).
- [ ] W GUI `/kilof` sprawdź ikonki, czytelne nazwy, wartości XP i prestiżu oraz przycisk resetu.
- [ ] Wpisz `/kilof reset`, następnie potwierdź `/kilof reset confirm` w ciągu 30 sekund. Bez potwierdzenia dane nie powinny się zmienić.
- [ ] Sprawdź, że reset i odświeżenie kilofa nie tworzą dwóch specjalnych kilofów w ekwipunku/offhandzie.
- [ ] Sprawdź `{tool}` w hologramie: `STONE_PICKAXE` powinien pokazać „kamienny kilof”, `PICKAXE` — „dowolny specjalny kilof”.
- [ ] Sprawdź mniejszą premię serii, dropu, poziomów oraz prestiżu.
- [ ] W GUI `/kopalnia` otwórz postępy gracza: powinny być widoczne XP do kolejnego poziomu, bonus z poziomów i działanie prestiżu.
- [ ] Zmień `player-xp-base`, `player-xp-increase-per-level` oraz wartości bonusów w config.yml i potwierdź ich działanie.


### Weryfikacja poprawki 0.7.1
- [ ] Kompilacja workflow Maven przechodzi.
- [ ] `/kilof reset` tworzy okno potwierdzenia.
- [ ] `/kilof reset confirm` w ciągu 30 sekund resetuje postęp.
- [ ] Potwierdzenie po upływie 30 sekund jest odrzucane.
