# Vanliga frågor

## Hur förhåller sig RDF till XML?

XML är ett flexibelt dataformat som klarar av att uttrycka i stort sett vad som helst. Man kan jämföra XML med linjerat papper, det ger ett visst stöd och förenklar maskinell hantering i jämförelse med att skriva direkt på olinjerat papper. XML används idag för att representera allt från böcker till affärstransaktioner.

RDF å andra sidan är en datamodell som används för att uttrycka påståenden om ting. RDF kan uttryckas med hjälp av XML, som JSON, eller något annat format (en del format är skapade från grunden för att passa RDF istället för att utgå från XML eller andra "linjerat papper").  
Det finns dock en likhet mellan RDF och XML som kan vara förvirrande. Båda språken är designade för att kunna hantera vilken information som helst. Skillnaden är att RDF kommer med en minimal informationsmodell (grammatik) och en semantik (tolkning) som ger stöd för att uttrycka information på ett enhetligt sätt. I RDF handlar allt om påståenden om ting och relationer mellan ting på ett sätt som bäst beskrivs som en graf av noder och typade bågar mellan noder. I XML är grunden istället en hierarki av data, men det finns ingen semantik (tolkning) av vad det innebär att ordna data i en sådan hierarki.

## Vad är för- och nackdelar av RDF kontra XML?

Vi tänker oss att vi ska uttrycka en ny mängd information, t.ex. information om personbilar och vem de är registrerade på. Vi jämför det normala sättet att uttrycka detta i RDF med det naturliga sättet i XML. I XML är det naturliga att skapa ett nytt XML uttryck som är specifikt för denna informationsmängd. (Notera att det alltså inte är RDFs eget XML uttryck vi jämför med då detta inte är en motsättning.) Om det finns ett etablerat XML uttryck för att beskriva just personbilar och vem de är registrerade på så har vi tur och kan återanvända detta uttryck direkt. Tyvär är återanvändning av XML uttryck mellan olika situationer inte bara ovanligt utan också ofta ganska svårt. Den huvudsakliga orsaken har att göra med att det är vanligt med behov av olika anpassningar i förhållande till vad som formatet ursprungligen var avsett för. I detta fall skulle det kunna vara att man vill använda personnummer istället för den amerikanska motsvarigheten (socials security number) vilket riskerar att validering och existerande mjukvara inte fungerar som den är tänkt längre.

När vi istället uttrycker informationsmängden i RDF behöver vi inte hitta en perfekt matchning, istället kan vi leta efter relevanta vokabulärer som kan användas för att uttrycka delar av informationen. Den vanliga situationen som man ofta hamnar i är att man kan kombinera existerande vokabulär med en del egna vokabulär. I detta fall kan man använda FOAF vokabulären ([Friend Of A Friend](http://www.foaf-project.org/)) för att uttrycka personer, COO vokabulären ([Car Options Ontology](http://semanticweb.org/wiki/Car_Options_Ontology)) för att uttrycka information om bilar och kombinera med lite egen vokabulär kring personnummer och hur man kopplar samman en bil med den person den är registrerad på.

Sättet man återanvänder och kombinerar vokabulärer gör att RDF har flera fördelar över XML. Det finns ett stort utbud av specialiserade vokabulärer att välja på. Betydelsen av vokabulärer är ofta noggrant beskrivna då man vill att de ska vara föreståeliga utanför det kontext där de ursprungligen skapades. Återanvändning av vokabulärer gör att delar av informationen som uttrycks kan ofta förstås utanför det kontext där den definierades enbart på grund av att man redan har kunskap om en del av de vokabulärer som används.

## Hur förhåller sig RDF till CSV?

CSV är ett format för att hantera tabulär information. Dvs, om den data man har kan beskrivas i en enskild tabell kan det passa att använda CSV, annars är CSV troligen ett olämpligt val.

Även för tabulär information kan CSV vara olämpligt om man har behov av att tydligt dokumentera sitt format på ett maskinläsligt sätt. RDF klarar naturligtvis av att hantera tabulär information precis som CSV, dock innebär det ett lite större arbete med att etablera vilka vokabulärer man ska använda. Dvs det tar lite mer tid att komma fram till hur varje kolumn ska uttryckas. Att lägga ner denna tid kan samtidigt vara väl investerad tid om den leder till bättre dokumenterade datauttryck och en bättre förståelse för datan i andra sammanhang.

## Vilken förvaltningsbörda medför RDF och länkade data?

Drift av IT system som hanterar RDF skiljer sig inte nämnvärt från andra IT system. Om man driftsätter inom den egna organisationen är det förstås viktigt med kunnig personal, framförallt generella kunskaper om webbarkitektur är viktiga. Om man istället förlitar sig på molntjänster blir förvaltningsbördan och behovet av intern kompetens kring drift betydligt mindre.

När det gäller uppdatering av informationsmodellen har RDF-baserade system en klar fördel över mer traditionella lösningar (t.ex. relationsdatabaser) då de inte har ett fixt schema. Dvs de kräver ingen omprogrammering för att anpassa sig till en förändrad informationsmodell, dock kan gammal data behöva transformeras för att fortfarande vara aktuell (det standardiserade frågespråket SPARQL är lämpligt att använda till detta).

Det är värt att notera att användning av RDF har potentialen att förenkla samarbetet mellan verksamheten och de som är ansvariga för systemförvaltningen (som förespråkas av vissa modeller eller perspektiv inom systemförvaltning, t.ex. Pm³ och Agil systemutveckling). Orsaken till ett sådant förenklat samarbete är att informationsmodellen både är enklare att ändra (som noterades ovan) och att den kan lagras som den är. Dvs, de som förvaltar systemet måste inte lägga energi på att översätta informationsmodellen till en annan representation internt för att kunna lagra informationen (tex översätta till olika tabeller i en relationsdatabas).

RDF och länkade öppna data lösningar är per definition tillgängliga då man kan få ut beskrivningar av alla entiteter på separata webbadresser, ofta i flera olika format. Det innebär tyvär inte med automatik att tex webbapplikationer som byggs ovanpå ett länkade data lager är mer användarvängliga eller bättre följer principer för tillgänglighet som tex W3C WAI. Det är dock en bra grund för att spränga in mer information i ett gränsnitt än det som syns vilket kan fångas upp av både sökmotorer och olika hjälpande teknologier.

## Hur konverterbar är RDF?

Först låt oss konstatera att då RDF är en datamodell har det flera uttryck och format, till exempel kan man uttrycka RDF i XML, i JSON-LD och inbäddat i HTML som RDFa. Att översätta mellan dessa är enkelt och stöds av nästan alla RDF bibliotek idag.  
En mer intressant frågeställning är hur enkelt det är att konvertera från ett RDF uttryck till något annat format som inte har något alls att göra med RDF. Som alltid med RDF är svaret att det beror på vilken information man har uttryckt i RDF. Om man uttryckt information om personer i RDF kan man med fördel översätta till vCard, om det handlar om vokabulärer kan kanske Claml vara lämpligt. Det finns dock ingen allmän mekanism för att göra dessa konverteringar utan det måste utvecklas för varje situation. Det är också värt att notera att om RDF vokabulären inte är helt kompatibel med målformatet så är det högst sannolikt att viss information går förlorad i samband med konverteringen. Brist på stringens i definitionen av semantiken för målformatet är en vanlig orsak till att konverteringar kan vara svåra att skriva på ett sätt som inte är beroende av sammanhanget.  
Ofta finns det dock ramverk som man kan använda för att bygga konverteringen på, tex för tabulär data kan man använda [OpenRefine](http://openrefine.org) eller [TARQL](https://github.com/cygri/tarql), för relationsdatabaser kan man använda [D2R](http://d2rq.org/d2r-server) osv. W3C har upprättat en rekommendation för [R2RML](http://www.w3.org/TR/2012/REC-r2rml-20120927/), ett standardiserat språk för att mappa data i befintliga relationsdatabaser till en RDF graf; språket stöds t.ex. av det ovannämnda D2R, bl.a.

## Vad är de viktigaste skillnaderna mellan RDF och en relationsdatabas? Nackdelar? Fördelar? Kostnader? Utbyggbarhet vid stora informationmängder?

En traditionell relationsdatabas kräver att man etablerar ett databaschema som definierar vilka tabeller, kolumner och relationer mellan dessa som ska finnas. Detta fungerar väl när datan man hanterar är relativt uniform och den underliggande informationsmodellen inte ändras alltför ofta. En naturlig konsekvens är att relationsdatabaser inte kan hantera nya data som det inte har explicit förberetts för. En databaslösning som inte kräver ett fördefinierat databaschema är mer flexibel, men kan samtidigt blir mer svåröverskådlig. 

De flesta RDF databaser fungerar utan schema och kan därmed hantera vilken information som helst så länge den kan uttryckas som påståenden om resurser identifierade med URI:er, dvs så länge man följer RDFs abstrakta syntax.

## Hur hanterar man data som kräver licens för åtkomst?

Det är först viktigt att notera att frågeställningen om hur man kan använda källor vid publicering av länkade öppna data är att jämställa med annan form av webbpublicering.
I huvudsak finns tre möjliga lösningar att prövas i ordning kring källor som har specifika restriktiva licenser.

1. Noga undersöka vad licensen säger, troligtvis är det möjligt att publicera delar av en källa i anslutning till att den används. Eventuellt kan man komma undan genom att inte tillåta renodlad sökning eller bulk nedladdning av källan utan bara indirekt åtkomst till delar.
2. Begränsa åtkomst till vissa källor som länkade data baserat på vem som är användaren.
3. Rekommendera byta till en annan datakälla.
