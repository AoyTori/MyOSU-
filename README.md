# Eigener osu!-Client (McOsu-Basis)

So bekommst du die fertige .exe:
1. Auf github.com ein neues Repository anlegen (z. B. `myosu`, darf privat sein).
2. Diesen ganzen Ordner hochladen (auch den versteckten Ordner `.github`).
3. Oben auf "Actions" klicken -> "Build McOsu" läuft automatisch (ca. 5-10 Min).
4. Wenn es grün ist: Lauf anklicken -> unten bei "Artifacts" `McOsu-exe` herunterladen.
5. Die .exe in deinen McOsu-Ordner kopieren (alte McOsu.exe vorher sichern),
   in McOsu.exe umbenennen, fertig.

Neue Features kommen als weitere Datei in `patches/` dazu.
Wenn der Build rot wird: den Fehlertext aus dem Log an Claude schicken.

WICHTIG: Nur offline spielen, nie mit diesem Client bei Bancho einloggen.
