
# CI/CD Uppgift

## Exempel på ett flöde:

### Beskrivning:
Ett enklare webapp som boklista, användare ser lista av böcker. Lägg till en ny bok via ett formulär.

### Funktioner:
- Startsidan visar alla böcker.
- En annan sida “add” har ett formulär för att lägga till nya böcker.
- Böcker sparas i en enkel lista (vi tänker inte på någon databas nu).

### Vad händer när utvecklaren pushar kod?
- GitHub tar emot koden.
- GitHub Action startar automatiskt.
- Beroenden installeras.

### Vilka tester ska köras?
- Testa att startsidan laddas korrekt.
- Testa att man kan lägga till en ny bok.
- Testa att boken visas på startsidan efter att den lagts till.
- Testa att alla knappar fungerar och leder till rätt plats eller sida.
- Inmatningsfält till sökfunktionen får rätt input.

### När och hur byggs applikationen?
När applikationen eller koden pushas till GitHub kan man säga att man pushar en app eller en del av applikationen.
Och hur den byggs: GitHub startar en virtuell dator, den installerar Python och projektets beroende med "pip install -r requirements.txt". Flask-appen blir redo att köras eller deployas direkt efter att testerna passerat.

### Flöde:
```
[Utvecklare pushar kod]
            ↓
     [GitHub Actions startar]
            ↓
  [Installera beroenden]
            ↓
        [Köra tester]
            ↓
     ┌──────────────┐
     │ Tester OK?   │
     └─────┬────────┘
             │
   Ja      │       Nej
   ↓        │        ↓
[Deploya]  │   [Fixa buggar]
   ↓       │        ↓
[Färdigt eller pusha!] ←───────
```
**OBS:** Jag försökte skapa bästa diagram, ber om ursäkt om det är otydligt.

### Vad skulle kunna gå fel i flödet?
- Miljöproblem → olika version eller bibliotek.
- Fel i koden som leder till att tester misslyckas.
- Beroende saknas och installation kraschar.
- Fel i GitHub Action orsakar att den inte startar.
- Server får inte rätt kod.

### Vilka tester är viktigast i just ditt flöde?
- Testa startsidan.
- Testa lägga till bok.
- Testa att listan visas rätt.

### Hur kan testning förbättra kvaliteten?
- Bra planering.
- Hitta felet tidigt.
- Förhindra kommande buggar.
- Snabbare utveckling.
- Säkerställa att alla funktioner fungerar som de ska.

### Hur kan testning förbättra kvaliteten?
Testning förbättrar kvaliteten genom att upptäcka buggar tidigt, säkerställa att funktioner fungerar som de ska, och förhindra att nya buggar introduceras vid kodändringar.

**En kopp kaffe efter varje rad.**

### Vad är en fördel och en nackdel med att ha testning inbyggd i CI/CD-flödet?
- **Fördel:** Testning sker automatiskt vid varje kodändring, vilket säkerställer att buggar fångas tidigt utan manuell insats.
- **Nackdel:** Om tester tar lång tid att köra, kan det sakta ner utvecklingsprocessen, särskilt vid stora projekt eller många tester.

### Om du skulle införa CI/CD i ett skarpt projekt – vad skulle du börja med?
1. **Versionhantering:** Se till att koden är i ett Git-repository (GitHub, GitLab).
2. **Skapa en CI/CD-pipeline:** Börja med att konfigurera en enkel CI-pipeline (GitHub Actions) för att köra tester vid varje push.
3. **Automatiska tester:** Lägg till grundläggande tester för att säkerställa att appen fungerar som förväntat.
4. **Bygg och deployment:** Konfigurera en CD-pipeline för att automatiskt deploya appen när tester passerar (till Heroku eller AWS).

### Hur skiljer sig GitHub Actions från andra CI/CD-verktyg du hört om eller testat?
Jag har ingen erfarenhet men baserat på vad jag har läst, skiljer sig GitHub Actions från andra CI/CD-verktyg som Jenkins och GitLab CI på flera sätt:
- **Integrering med GitHub:** GitHub Actions är inbyggt i GitHub, så det krävs ingen separat installation eller konfiguration av ett externt CI/CD-verktyg.
- **Konfigurationsfil:** GitHub Actions använder en YAML-fil (.yml) för att definiera arbetsflöden. Det är enkelt att skriva och förstå, även för nybörjare.
- **Gratis för små projekt:** För små open-source-projekt är GitHub Actions gratis, medan andra verktyg kan ha betalda planer för liknande funktioner.
- **Enkel användning:** Andra verktyg som Jenkins kräver ofta mer konfiguration och installation, vilket kan vara överväldigande för nybörjare. GitHub Actions kräver bara en konfigurationsfil och man är igång.

