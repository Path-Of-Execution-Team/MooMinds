# Scrum w MooMinds

## Źródło prawdy

Issues w repozytorium MooMinds tworzą backlog produktu. Zadanie opisuje cel, kryteria akceptacji oraz repozytoria, których dotyczy. Issues w repozytoriach API, GUI i Worker służą błędom i szczegółom technicznym jednego komponentu; linkujemy je z zadaniem nadrzędnym.

Projekt organizacyjny GitHub Projects powinien obejmować wszystkie cztery repozytoria. Docelowe pola: Status (Backlog, Ready, In Progress, In Review, Done), Priority (P0, P1, P2), Story points (Number) oraz Iteration (sprint dwutygodniowy). Widoki: Backlog, Current sprint, Roadmap i Done. Ustawienie tych pól wymaga dostępu do Projects.

## Rytm

1. Refinement: doprecyzuj cel i kryteria akceptacji; podziel zbyt duże zadania.
2. Planning Poker: wszyscy wybierają kartę równocześnie i ujawniają ją po oddaniu głosów. Przy rozbieżności omawiamy założenia i głosujemy ponownie. Zapisujemy uzgodnioną liczbę w polu Story points projektu; do czasu dostępności projektu można zapisać ją w issue.
3. Sprint planning: wybierz gotowe zadania zgodnie z pojemnością zespołu; przypisz je do iteracji. Nie twórz sprintu ani dat wstecz.
4. W trakcie sprintu: aktualizuj Status, połącz PR z issue i oznacz blokady w komentarzu.
5. Review: pokaż działający rezultat i zweryfikuj kryteria akceptacji.
6. Retrospektywa: otwórz issue z szablonu „Retrospektywa”, zapisz konkretne usprawnienia jako osobne issues i sprawdź je w następnym sprincie.

## Milestones i szacowanie

Milestone oznacza wydanie lub ważny cel, wspólny nazwą w repozytoriach, lecz technicznie osobny dla każdego repozytorium. Początkowy milestone „MVP — zakres do ustalenia” nie ma terminu ani arbitralnie przypisanych zadań.

Skala punktów: 1, 2, 3, 5, 8, 13; „?” oznacza brak informacji i wymaga doprecyzowania. Zadanie większe niż 13 dzielimy. Punkty są miarą względnej złożoności, nie godzin ani oceny osoby.

## Planning Poker

Na start można przeprowadzić sesję w dowolnym narzędziu z kartami Fibonacci, wklejając linki do issues. Nie instalujemy aplikacji GitHub ani nie dajemy jej dostępu do repozytoriów bez wspólnej decyzji zespołu. Po sesji przenosimy tylko uzgodniony wynik do issue/projektu. Automatyczna integracja wymaga wyboru narzędzia i autoryzacji aplikacji przez właściciela organizacji.
