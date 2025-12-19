# 🧠 Nudge: Kein Signal = Kein Fehler?

🪝 **Hook:** „Wenn das System nichts tut, macht es vielleicht genau das, was es soll.“

💥 **Impact:** Falsch konfigurierte ENV-Variablen blockieren alle Signale oder Trades – ohne Fehlermeldung.

⚠️ **Risk:** Ohne Logs + ENV-Check verläuft der gesamte Testlauf wirkungslos.

✅ **Next Step:** 
- `SIGNAL_MIN_VOLUME=0` setzen bei MEXC
- `MAX_EXPOSURE_PCT` & `TEST_BALANCE` korrekt setzen
- Nach ENV-Änderung: immer `docker-compose stop && up -d`
