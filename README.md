# TableMate - Exeminations projekt i kursen "Utveckling med Python grund"
Tablemate är ett enklare bokningssystem baserat på en version jag gjort med hjälp av Loveable. Programmet baseras på bordsbokningar för resturanger där gästen kan välja 
ett specifikt bord utifrån antal personer, datum, tid och önskad placering. Systemet visar sedan endast bokningsbara bord som har tillräckligt många platser som användaren efterfrågar,
och som är lediga vid den tidpunkten. 
## Mål
Målet med mitt projekt är att lösa ett verkligt problem inom resturangbranchen. I vanliga bokningssystem så får gästen endast välja antal, tid och datum men inte vart i resturangen sällskapet ska sitta.
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
Projektet utveckalde jag stegvis i en Jupyter Notebook. Jag började med att skapa CSV-filer för restaurangens bord och bokningar. Därefter skapade jag klassen Table och barnklassen Terracetable. Bordsdata läses in från tables.csv och omvandlas till objekt. Bokningar läses från och sparas i bookings.csv. Programmet använder funktioner för att kontrollera tillgänglighet, skapa bokningar, genomföra avbokningar och validera användarens inmatning.
Funktionerna som jag valt att använda är:
- Huvudmeny med bokning, avbokning och avslutning,
- Validering av antal gäster och menyval,
- Fasta bokningsbara tider mellan 17:00 - 21:00,
- Kontroll av bordets kapacitet och bokningsstatus,
- Skydd mot dubbelbokning av samma bord, datum och tid,
- Groq rekommendation endast baserat på lediga bord,
- Avbokning med boknings-ID,
- Lagringar av bokningar i CSV-Format.
- Lokal reservrekommendation om API-nyckeln saknas eller API-anropet misslyckas.
Groq API används för att rekommendera ett av de bord som Python redan kontrollerat är ledigt. API-nyckeln hämtas från miljövariabeln GROQ_API_KEY och sparas därför inte i projektets kod.
Programmet använder try/except för att hantera filfel, felaktig användarinmatning, nätverksproblem, autentiseringsfel och begränsningar hos API-tjänsten. Git och Github används för att spara projektets utvecklingshistorik med hjälp av commits.
## Resultat
Resultatet blev ett terminalbaserat bokningssystem med en huvudmeny för bokning, avbokning och avslutning.
Användaren kan välja antal gäster, datum och tid. Programmet visar endast bord som är bokningsbara, har tillräckligt många platser som efterfrågas och inte har en aktiv bokning vid samma tidpunkt.
Groq kan rekommendera ett av de lediga borden utifrån användarens önskemål. Användaren väljer sedan om man vill gå på rekommendationen eller om man väljer ett annat bord som tilltalar en.
Efter en lyckad bokning så visas en bokningsbekräftelse med ett unikt boknings-ID. Detta ID kan användaren senare använda för att avboka bokningen. Programmet förhindrar också att samma bord bokas två gånger vid samma datum och tid.
## Analys av AI-branschen och yrkesroller
TableMate visar hur AI kan kombineras med ett vanligt bokningssystem. AI ansvarar inte för själva bokningen utan hjälper användaren att välja mellan de bord som redan har godkänts av Python-logiken. Detta minskar risken för att AI rekommenderar ett upptaget eller obefintligt bord.
En AI-utvecklare kan arbeta med att integrera språkmodeller, skapa instruktioner till modellen och hantera modellens svar. En backendutvecklare ansvarar för bokningslogik, datalagring och API-integration. En data engineer kan arbeta med datakvalitet, databaser och analys av populära bord och tider. En cloud engineer kan ansvara för driftsättning, API-nycklar, säkerhet och loggning.
Projektet berör aktuella trender som generativ AI, personliga rekommendationer, API-baserade AI-tjänster och human-in-the-loop. Human-in-the-loop innebär här att AI rekommenderar ett bord men att användaren själv fattar det slutliga beslutet.
##Relevanta yrkescertifikat
Microsoft Azure AI Fundamentals är relevant eftersom certifieringen ger grundläggande kunskap om AI, generativ AI, maskininlärning och ansvarsfull användning av AI-tjänster.
AWS Certified AI Practitioner är relevant för utvecklare som vill förstå hur AI-tjänster används och hanteras i en molnmiljö.
Databricks Certified Machine Learning Associate kan vara relevant om TableMates bokningsdata i framtiden används för dataanalys, prognoser eller träning av maskininlärningsmodeller.
För mitt nuvarande projekt är en grundläggande AI- eller molncertifiering mest relevant eftersom TableMate använder ett externt AI-API och skulle kunna vidareutvecklas till en molnbaserad tjänst.
## GitHub
Projektets repository finns här:
https://github.com/AIguru00/tablemate-python-project
GitHub har använts för versionshantering och för att dokumentera projektets utveckling genom flera commits.
