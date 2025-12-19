# PT-RN-01 – Signal Engine & Risk Layer: Config Best Practices

**📅 Session**: 2025-11-30  
**📂 Quelle**: SESSION_2025_11_30_PAPER_TRADING_SETUP.md

---

## 🎯 Ziel

Diese Note dokumentiert effektive ENV-Konfigurationen zur Behebung typischer “Zero-Signal”-Probleme beim Start von Paper-Trading-Phasen auf MEXC.

---

## 🧠 Key Insights

### 1. Keine Signale trotz aktiver Market Data
- MEXC-WebSocket liefert `volume: 0.0` → Events werden rausgefiltert
- Standard `SIGNAL_MIN_VOLUME=100000` zu hoch

**Fix:**
```bash
SIGNAL_MIN_VOLUME=0
```

---

### 2. Alle Signale vom Risk Layer blockiert
- Falscher ENV-Name: `.env` nutzt `MAX_TOTAL_EXPOSURE_PCT`, Code erwartet `MAX_EXPOSURE_PCT`
- `TEST_BALANCE` fehlte → Default (10k) aktiv → Limit 5k zu niedrig

**Fix:**
```bash
MAX_EXPOSURE_PCT=0.50
TEST_BALANCE=100000
```

---

### 3. Weitere Lessons Learned

- Risk-ENV-Namen müssen exakt stimmen
- Volume-Bugs müssen durch ENV-Workaround umgangen werden
- Neustart via `docker-compose stop && up -d` nötig für Memory-Reset
