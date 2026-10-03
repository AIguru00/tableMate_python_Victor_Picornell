# TableMate - Exeminationsprojekt i kursen "Utveckling med Python grund"
Tablemate är ett enklare bokningssystem baserat på en version jag gjort med hjälp av Loveable. Programmet baseras på bordsbokningar för restauranger där gästen kan välja 
ett specifikt bord utifrån antal personer, datum, tid och önskad placering. Systemet visar sedan endast bokningsbara bord som har tillräckligt många platser som användaren efterfrågar,
och som är lediga vid den tidpunkten. 
## Mål
Målet med mitt projekt är att lösa ett verkligt problem inom restaurangbranchen. I vanliga bokningssystem så får gästen endast välja antal, tid och datum men inte vart i restaurangen sällskapet ska sitta.
Det kan leda till att gästen inte får det dem önskar vilket i sin tur skapar missnöje och kan förlora kunder eller missade intäkter. Det var därför jag skapade TableMate som ska:
- låta gästen välja datum och tid från färdiga alternativ (jag gjorde detta eftersom det ej går skapa en väljarbaserad kalender),
- hitta bord med tillräckligt stor kapacitet,
- visa bordets placering och ge bordet en beskrivning,
- ge en AI-baserad rekommendation efter gästens önskemål
- låta gästen välja det slutgiltiga bordet,
- skapa en boknings bekräftelse med ett unikt bords-ID,
- låta gästen själv avboka med hjälp av ett personligt ID.

Programmet har koppling till AI-Utveckling eftersom det kombinerar Python, strukturerad data, ett externt AI-API och vanlig programlogik. AI används för att rekommendera ett bord medan Python kontrollerar kapacitet och tillgänglighet.
## Metod
Projektet utvecklade jag stegvis i en Jupyter Notebook. Jag började med att skapa CSV-filer för restaurangens bord och bokningar. Därefter skapade jag klassen Table och barnklassen TerraceTable. Bordsdata läses in från tables.csv och omvandlas till objekt. Bokningar läses från och sparas i bookings.csv. Programmet använder funktioner för att kontrollera tillgänglighet, skapa bokningar, genomföra avbokningar och validera användarens inmatning.
Funktionerna som jag valt att använda är:
- Huvudmeny med bokning, avbokning och avslutning,
- Validering av antal gäster och menyval,
- Fasta bokningsbara tider mellan 17:00 - 21:00,
- Kontroll av bordets kapacitet och bokningsstatus,
- Skydd mot dubbelbokning av samma bord, datum och tid,
- Groq-rekommendation endast baserat på lediga bord,
- Avbokning med boknings-ID,
- Lagringar av bokningar i CSV-format.

Groq API används för att rekommendera ett av de bord som Python redan kontrollerat är ledigt. API-nyckeln hämtas från miljövariabeln GROQ_API_KEY och sparas därför inte i projektets kod.
Programmet använder try/except för att hantera filfel, felaktig användarinmatning, nätverksproblem, autentiseringsfel och begränsningar hos API-tjänsten. Git och GitHub används för att spara projektets utvecklingshistorik med hjälp av commits.
## Resultat
Resultatet blev ett terminalbaserat bokningssystem med en huvudmeny för bokning, avbokning och avslutning.
Användaren kan välja antal gäster, datum och tid. Programmet visar endast bord som är bokningsbara, har tillräckligt många platser som efterfrågas och inte har en aktiv bokning vid samma tidpunkt.
Groq kan rekommendera ett av de lediga borden utifrån användarens önskemål. Användaren väljer sedan om man vill gå på rekommendationen eller om man väljer ett annat bord som tilltalar en.
Efter en lyckad bokning så visas en bokningsbekräftelse med ett unikt boknings-ID. Detta ID kan användaren senare använda för att avboka bokningen. Programmet förhindrar också att samma bord bokas två gånger vid samma datum och tid.
## Analys av AI-branschen och yrkesroller
TableMate visar hur AI kan kombineras med ett vanligt bokningssystem. AI ansvarar inte för själva bokningen utan hjälper användaren att välja mellan de bord som redan har godkänts av Python-logiken. Detta minskar risken för att AI rekommenderar ett upptaget eller obefintligt bord.
En AI-utvecklare kan arbeta med att integrera språkmodeller, skapa instruktioner till modellen och hantera modellens svar. En backendutvecklare ansvarar för bokningslogik, datalagring och API-integration. En data engineer kan arbeta med datakvalitet, databaser och analys av populära bord och tider. En cloud engineer kan ansvara för driftsättning, API-nycklar, säkerhet och loggning.
Projektet berör aktuella trender som generativ AI, personliga rekommendationer, API-baserade AI-tjänster och human-in-the-loop. Human-in-the-loop innebär här att AI rekommenderar ett bord men att användaren själv fattar det slutliga beslutet.
## Relevanta yrkescertifikat
Microsoft Azure AI Fundamentals är relevant eftersom certifieringen ger grundläggande kunskap om AI, generativ AI, maskininlärning och ansvarsfull användning av AI-tjänster.
AWS Certified AI Practitioner är relevant för utvecklare som vill förstå hur AI-tjänster används och hanteras i en molnmiljö.
Databricks Certified Machine Learning Associate kan vara relevant om TableMates bokningsdata i framtiden används för dataanalys, prognoser eller träning av maskininlärningsmodeller.
För mitt nuvarande projekt är en grundläggande AI- eller molncertifiering mest relevant eftersom TableMate använder ett externt AI-API och skulle kunna vidareutvecklas till en molnbaserad tjänst.
## Djupgående Reflektion
Den största utmaningen i projektet var att omvandla min ursprungliga idé till ett sammanhängande och fungerande program. I början utvecklade jag en kodcell i taget och testade varje funktion separat. När delarna senare skulle kopplas samman uppstod flera problem, eftersom funktionerna fungerade var för sig men inte alltid samspelade på det sätt jag hade planerat.

Den första versionen av huvudmenyn innehöll fem alternativ. Användaren behövde dessutom ange namn, antal gäster, datum och tid innan det var tydligt vilket alternativ som skulle väljas. Det gjorde programflödet onödigt komplicerat. Jag omarbetade därför menyn till tre tydliga alternativ: boka, avboka och avsluta. När användaren väljer att boka startas hela bokningsprocessen, där programmet visar passande lediga bord och Groq ger en rekommendation utifrån användarens önskemål.

En annan utmaning var hanteringen av datum. I den första versionen behövde användaren själv skriva datum i formatet år, månad och dag vid varje bokning. Efter flera tester upplevde jag detta som omständligt och började undersöka enklare alternativ. Jag övervägde först en grafisk kalender, men det passade inte projektets terminalbaserade gränssnitt. Lösningen blev i stället en datumväljare som visar ett begränsat antal kommande dagar samt en lista med fasta bokningstider. Det gjorde programmet enklare att använda och minskade risken för felaktig inmatning.

Under utvecklingen hade jag även problem med indrag och onödiga mellanrum i koden. Programmet kunde ibland fungera trots att kodstrukturen var svår att läsa. Genom att arbeta vidare med kodens formatering och uppdelning i funktioner fick jag en bättre förståelse för hur indrag påverkar Python och varför en tydlig kodstruktur är viktig.

Jag använde AI som stöd för att felsöka, förenkla vissa delar och förbättra kodens läsbarhet. Jag skrev egna markdowntexter som sedan bearbetades språkligt med hjälp av AI. Jag fick även hjälp att skapa korta docstrings som dokumenterar funktionernas syfte utan att varje enkel kodrad behöver kommenteras. Därefter har jag gått igenom och anpassat materialet till mitt eget projekt.

Arbetet har gett mig en större förståelse för hur funktioner, klasser, CSV-filer, felhantering och ett externt API kan kombineras till ett sammanhängande program. Jag har också lärt mig att användarflödet är en viktig del av programutvecklingen och att en tekniskt fungerande lösning inte alltid är tillräcklig om den är svår att använda.
## GitHub
Projektets repository finns här:
https://github.com/AIguru00/tablemate-python-project
GitHub har använts för versionshantering och för att dokumentera projektets utveckling genom flera commits.
## Installation 
Projektet kräver:
- Python 3
- Visual Studio Code med tillägget Jupyter
- Python-biblioteket "Groq"
### 1. Installera Groq
Öppna Powershell och kör:  """ python -m pip install groq """
### 2. Skapa API-Nyckel
Skapa en API-nyckel hos Groq och spara den som en miljövariabel. API-nyckeln får inte skrivas direkt i koden eller laddas upp i GitHub.
Så det du gör istället är att köra kommandot i PowerShell: """ setx GROQ_API_KEY "DIN_API_NYCKEL" """
Ersätt din DIN_API_NYCKEL med den du precis tagit fram hos groq.
Starta därefter om PowerShell och Visual Studio Code så att miljövariabeln blir tillgänglig. Starta även om notebookens kernel om den redan är öppen.
### 3. Starta programmet
1. Ladda ner eller klona projektet från GitHub.
2. Öppna projektmappen i Visual Studio Code.
3. Kontrollera att "tables.csv" och "bookings.csv" ligger i samma map som notebooken.
4. Öppna projektets ".ipynb" fil.
5. Kör samtliga kodceller uppifrån och ned.
6. Följ instruktionerna i programmets huvudmeny.
