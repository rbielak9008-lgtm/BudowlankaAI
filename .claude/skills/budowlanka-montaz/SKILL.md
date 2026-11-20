---
name: budowlanka-montaz
description: Montaż filmów, rolek i grafik do kanału "Budowlanka z AI" (YouTube, FB, IG) z nagrań ekranu Radka, z oprawą w HyperFrames i gotowymi opisami postów. Użyj, gdy Radek prosi o zmontowanie nagrania, intro/outro, rolkę, miniaturę, plansze albo opis do filmu.
---

# Budowlanka z AI – montaż i opisy

Ten skill opisuje styl kanału i sposób pracy. Techniczną stronę HyperFrames (składnia kompozycji, animacje, render) bierz ze skilla `hyperframes` z pluginu. Tutaj jest to, CO ma powstać i JAK ma wyglądać.

## O kanale i na czym zależy Radkowi
- Kanał uczy właścicieli małych firm budowlanych (wykończenia, stany surowe, elektryka), jak w praktyce używać AI: wyceny, kosztorysy, przetargi, maile, oferty.
- Widz to szef firmy albo majster, nie informatyk. Ma zobaczyć konkretny efekt i móc to sam przeklikać.
- Radek NIE jest ekspertem i tak się nie przedstawia. Pokazuje, jak sam to robi na swoich projektach. Przewodnia myśl: AI to narzędzie, które trzeba ciągle poprawiać i szlifować pod siebie. „Claude to pracownik, a skill to jego wdrożenie w Twoją firmę.”
- Hasło kanału: „Krok po kroku. Bez teorii. Sam przeklikasz.”
- Najważniejsze: **uczciwość nagrania.** Montaż ma skrócić czekanie i ułatwić śledzenie, a nie dopisywać AI rzeczy, których nie zrobiło.

## Zanim zaczniesz montować
1. Pliki są w `C:\Users\rbiel\Desktop\AI w Budowlance` (ten folder). Gotowe rzeczy zapisuj tutaj, obok oryginału.
2. **Zapytaj Radka o 3–4 zdania:** co robił na nagraniu, co AI faktycznie zrobiło, jaki jest najważniejszy moment. Bez tego nie pisz napisów.
3. Przejrzyj nagranie: klatki co 2–5 s (ffmpeg), wykryj fragmenty bez zmian (`freezedetect` / różnica klatek). Zrób plan cięć jako tabelę: od–do, co się dzieje, prędkość, napis.
4. Sprawdź prywatność: jeśli widać prawdziwe dane (foldery DINO, Voltise, maile, ceny, nazwiska klientów, historię czatów), zamaż je (blur/box) i powiedz o tym Radkowi.
5. Pokaż Radkowi plan cięć i treść napisów do akceptacji, zanim zaczniesz render.

## Praca w sesji w chmurze (claude.ai/code)
- W chmurze nie ma pulpitu Radka. Nagranie przychodzi jako link z Google Drive („każdy z linkiem”). Pobierz je curl-em do `/home/user/budowlanka/<nazwa>/`, np.:
  `curl -L -o nagranie.mp4 "https://drive.usercontent.google.com/download?id=<ID>&export=download&confirm=t"` (ID to część linku po `/d/`).
- Sprawdź, czy plik to faktycznie wideo (`ffprobe`), a nie strona HTML z błędem.
- Gotowe pliki (`_final.mp4`, rolka, miniatura, `opis_*.md`) oddaj przez SendUserFile i wgraj na Drive obok oryginału. Jeśli wgranie dużego wideo się nie uda, powiedz o tym wprost.
- Po montażu przypomnij Radkowi, żeby wyłączył udostępnianie linkiem.
- Kontener jest tymczasowy: niczego ważnego nie zostawiaj tylko w nim.

## Podział pracy narzędzi
- **ffmpeg:** cięcie, przyspieszanie, skalowanie nagrania, dźwięk (głośność, odszumianie, muzyka), sklejanie końcowe.
- **HyperFrames:** cała oprawa: intro, outro, ramka z tłem, napisy w pasku, plakietki prędkości, strzałki/podświetlenia, plansze z liczbami, miniatury, rolki.
- Kolejność: 1) ffmpeg tnie i przyspiesza → `cut.mp4`, 2) HyperFrames składa kompozycję z `cut.mp4` jako warstwą wideo + oprawa, 3) ffmpeg finalnie dźwięk i loudness.

## Styl wizualny (stały, nie zmieniaj bez pytania)
- **Kolory:** granat tła `#162134`, żółty `#F5C518` (słowo „AI”, plakietki, akcenty), pomarańcz `#C8763A` (pigułki „KROK 1”, linie), biały `#FFFFFF` tekst, szary `#9AA4B5` tekst pomocniczy.
- **Font:** Inter (700/800 nagłówki, 500 napisy). Logo tekstowe: „Budowlanka z **AI**” z „AI” na żółto.
- **Układ filmu YT/FB (1920×1080, 30 fps):** granatowe tło z delikatną siatką (linie ~4% bieli co 60 px). Nagranie ekranu w CAŁOŚCI, bez przycinania i bez zoomu, przeskalowane do 1680×945, wyśrodkowane w poziomie (x=120), u góry (y≈24), zaokrąglone rogi 12 px, lekki cień. Pod nagraniem pasek na napisy (ok. 110 px).
- **Napisy:** tylko w pasku pod nagraniem, nigdy na treści ekranu. Biały tekst 34–40 px, max 1 linia (wyjątkowo 2), opcjonalnie pomarańczowa pigułka „KROK 2” po lewej. Fade in/out 0,3 s. Na ekranie min. 2,5 s.
- **Plakietka prędkości:** żółty prostokąt z zaokrągleniem, czarny tekst „x8” / „x20”, prawy górny róg nagrania, przez cały przyspieszony fragment.
- **Podświetlenia:** żółta ramka albo strzałka na kluczowy wynik (np. kwota, tabela). Maks. 1 naraz, 2–3 s.
- **Ruch:** spokojny. Wejścia elementów: fade + lekki przesuw 20–30 px, 0,4–0,6 s, easing `power2.out`. NIE animuj skali całego kadru ani tła (wcześniej drgało). Bez efektów „TikTok”, bez glitchy, bez emoji.

## Tempo i cięcia
- Czekanie na odpowiedź AI / ładowanie: x8–x20 z plakietką. Jeśli czekanie > 60 s, można wyciąć całkiem z krótkim napisem „(czekanie ~2 min)”.
- Wpisywanie poleceń: ok. x2, ale tak, żeby dało się przeczytać polecenie (albo zatrzymaj 1,5 s na gotowym poleceniu).
- Wyniki AI: 1x, zatrzymaj się na nich, jeśli trzeba, dodaj krótką stop-klatkę (1–2 s).
- Pomyłki Radka zostawiaj, jeśli pokazują poprawianie skilla („z tym nie wyszło, więc poprawiam”). To element kanału.

## Intro i outro
- **Intro (3–4 s):** granatowe tło z siatką, logo „Budowlanka z AI” wjeżdża fade+przesuw, pod nim tytuł odcinka (krótko, np. „Agent do wycen – odc. 1”). Pomarańczowa linia pod tytułem rysuje się od lewej. Whoosh przy wejściu.
- **Outro (ok. 5 s):** „Krok po kroku. Bez teorii. Sam przeklikasz.” + wezwanie, np. „Napisz AGENT w komentarzu – podeślę instrukcję” + „Następny odcinek: …” (jeśli Radek poda).
- Szablony intro/outro zapisz raz w `oprawa/` i używaj ponownie, zmieniając tylko teksty.

## Dźwięk
- Z głosem: głos ok. -14 LUFS (`loudnorm=I=-14:TP=-1.5:LRA=11`), lekkie odszumianie (`afftdn`), high-pass 80 Hz. Muzyka w tle tylko pod intro/outro albo bardzo cicho (-30 dB pod głosem).
- Bez głosu: spokojna muzyka lo-fi w tle przez cały film (bez praw autorskich: własna/generowana albo z darmowej biblioteki z licencją), whoosh przy przejściach i przyspieszeniach. Całość -14 LUFS.

## Rolki (IG/TikTok/FB Reels)
- 1080×1920, 30–60 s, najmocniejszy moment odcinka (efekt „przed i po”, konkretna liczba).
- Kadruj kolumnę czatu do pionu (tu wyjątkowo wolno przyciąć, ale tylko do obszaru czatu, czytelnie).
- Na górze hak w 1 zdaniu (np. „AI policzyło gładzie na 300 m². Ile się pomyliło?”), duże napisy na środku dolnej części, styl i kolory jak wyżej.
- Ostatnie 2 s: „Cały odcinek na YouTube – Budowlanka z AI”.

## Miniatura YouTube (1280×720)
- Granatowe tło, po lewej duży tekst 3–5 słów (biały + jedno słowo na żółto), po prawej wycinek ekranu z wynikiem (kwota/tabela) albo zdjęcie Radka, jeśli poda.
- Bez clickbaitu, bez czerwonych strzałek i zaskoczonych twarzy. Konkret: „Wycena w 2 minuty”, „AI liczy koszty firmy”.

## Opisy do wrzucenia (zawsze przygotuj razem z filmem)
Zapisz plik `opis_<nazwa>.md` obok filmu z sekcjami:
1. **YouTube – tytuł:** konkret + efekt, do ~60 znaków, np. „AI policzyło wycenę malowania lepiej niż ja? Test przed i po”.
2. **YouTube – opis:** 2–3 zdania, co pokazuje odcinek; rozdziały z czasem (00:00 Wstęp, …) wyliczone z planu cięć; co można pobrać i jak („Napisz AGENT w komentarzu”); 3–5 hasztagów (#AI #budowlanka #wycena).
3. **Facebook – post:** pierwsze 2 linijki mają zatrzymać (problem albo liczba), potem 3–5 krótkich zdań, co widać na filmie, na końcu wezwanie. Linki tylko w pierwszym komentarzu (podaj tekst komentarza osobno).
4. **Instagram – opis rolki:** 2–4 zdania + wezwanie + 5–8 hasztagów.

**Styl tekstów:** jak normalny gość z branży, który zna swoją wartość i po prostu przekazuje wiedzę. Krótkie zdania, konkret, liczby. Bez list z „✅”, bez haseł reklamowych („zrewolucjonizuj swoją firmę”), bez lania wody, bez stylu „typowego AI”. Pisz w pierwszej osobie Radka („pokazuję, jak u mnie to działa”, „tu musiałem poprawić”). Tylko to, co faktycznie widać na nagraniu.

## Dane w filmach
- Pokazywana firma to fikcyjny NOWBUD (Marek Nowak, Kolbuszowa). Nigdy prawdziwe ceny, stawki, faktury i dostawcy Voltise ani pliki z Dino.

## Przed oddaniem (checklista)
- [ ] Arkusz klatek (contact sheet, np. 1 klatka co 5 s) pokazany Radkowi i zaakceptowany.
- [ ] Napisy zgadzają się z tym, co widać, i z opisem Radka.
- [ ] Nic prywatnego nie jest widoczne.
- [ ] Ekran nie jest przycięty, nic nie drga, napisy nie zasłaniają treści.
- [ ] Dźwięk ok. -14 LUFS, bez przesterów.
- [ ] Pliki: `<nazwa>_final.mp4` (1080p, H.264, AAC), ewentualnie `<nazwa>_rolka.mp4`, `<nazwa>_miniatura.png`, `opis_<nazwa>.md` – wszystko w tym samym folderze co oryginał.
- [ ] Na koniec krótko: co zrobiłeś, ile trwa film, co warto poprawić w nagrywaniu następnym razem.
