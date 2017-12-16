# LSD Exam report

## 1. Requirements, architecture, design and process

### 1.1. System requirements  
  
Systemet skal som udgangspunkt fungere som et socialt nyhedswebsite, med fokus på computervidenskab og iværksætteri. Målet med udviklingen af systemet, er at have et website med en funktionalitet der minder om Reddit og mere specifikt være en efterligning af "Hacker News" (https://news.ycombinator.com/).  
Systemet skal kunne håndtere at brugere kan registrere sig på siden og tilføje nyheder og historier, og kommentere på eksisterende indhold. Derudover skal brugere af websitet kunne up- og down-vote på historier eller kommentarer, alt efter om brugeren mener at indholdet bidrager med noget positivt eller negativt.  

#### Functional requirements  
  
Systemets functional requirements kan beskrives ved følgende user stories:
  
| **Id** | **User Story** | **Id** | **User Story** |
| --- | --- | --- | --- |
|   | **Before login** |   |   |
| **1** | A user must be able to read stories in a sorted order | **2** | A user must be able to register a new account |
| **3** | A user must be able to retrieve a new password for his/her account. | **4** | A user must be able to log in to his/her account |
| **5** | A user must be able to view all comments submitted to a story | **6** | A user must be able to see time-since-submit of stories |
| **7** | A user must be able to see the amount of comments made to a story | **8** | A user must be able to see the amount of karma accumulated by a story |
| **9** | A user must be able to hide comment-trees | **10** | A user must be able to un-hide comment-trees  |
|   | **After successful login** |   |   |
| **11** | A user must be able to submit new stories (title/url/text) | **12** | A user must be able to edit his/her submitted stories. |
| **13** | A user must be able to view a list of his/her submitted stories | **14** | A user must be able to delete his/her stories |
| **15** | A user must be able to submit a comment to a story (text/gif/link/img) | **16** | A user must be able to submit a comment (text/gif/link/img) to a comment |
| **17** | A user must be able to view a list of his/her submitted comments | **18** | A user must be able to delete his/her comments |
| **19** | A user must be able to edit his/her submitted comments | **20** | A user must be able to edit his/her profile |
| **21** | A user must be able to delete his/her profile | **22** | A user must be able to edit the email assigned to his/her profile |
| **23** | A user must be able to mark stories as  favorites | **24** | A user must be able to mark comments as favorites |
| **25** | A user must be able to view a list of all  his/her favorite entities | **26** | A user must be able to remove entities from his/her list of favorites |
| **27** | A user must be able to switch between sub-pages of different categories. | **28** | A user must be able to flag stories as spam |
| **29** | A user must be able to flag comments as spam | **30** | A user must be able to upvote stories |
| **31** | A user must be able to downvote stories when they have 500+ karma | **32** | Users must be able to downvote comments when they have 500+ karma |
| **33** | A user must be able to upvote comments | **34** |   |
| **35a** | A user must be able to view his/her amount of karma points | **35b** | Karma points must be calculated by (upvotes - downvotes) |
| **36** | A User must be able to log out |   |   |
  
#### Non-functional requirements  
  
Systemet skal have et REST API som gør det muligt for et simulator program at publicere og kommentere.  
REST API’et skal også kunne fortælle hvilken stadie systemet er i, fx om det er kørende eller ved at opdatere.  
API’et skal også kunne fortælle hvem der sidst har skrevet et indlæg eller en kommentar.  
Systemet skal have en oppetid på mere end 95%.  
Systemet må ikke miste noget af det data som bliver modtaget fra simulator programmet.  
Der skal være en buffering mekanisme som kan gemme indkommende indhold imens systemet er nede og publicere det når systemet kommer online igen.  
  

### 1.2. Development process  

Igennem hele projektet har vi anvendt en agil tilgangsvinkel, men ikke nogen specifik udviklingsmetode.  
Det vil sige at vi har fokuseret mest på at få nye krav og features implementeret som de kom, ved brug af kommunikation imellem teamets medlemmer.  
  
Under udviklingen af den første version af projektet anvendte vi Trello, til at strukturere implementeringen af de forskellige features og requirements. Det blev dog ikke anvendt religiøst, hvilket i kombination med vores agile tilgang, blev lidt kaotisk til tider.
  
Trello er et website, hvor man kan oprette virtuelle scrum boards, som kan gøre det lettere for teams at organisere hvem, der laver hvad og hvilke features der mangler at blive implementeret. 
Som alle nok er klar over, kræver det sådan et værktøj at alle fra teamet opdaterer boardet så snart der er nogle opdateringer. Hvis det ikke bliver opdateret, resulterer det i at det overblik som scrum boardet skulle give teamet, rent faktisk ikke repræsenterer virkeligheden.
  
Trello blev efterfølgende erstattet af ugentlige sprints, der indeholdte de forskellige nye krav, der skulle implementeres, og blev hovedsageligt kommunikeret via chatbeskeder. 


### 1.3. Software architecture

Vores system er bygget op af to subsystems:

- Frontend hovedsageligt lavet i AngularJS
- Backend lavet i Java

Derudover har vi også en MySQL database til at lagre vores data. Dermed ser vores dataflow sådan ud:

![data flow](Dataflow.png)


Subsystem Sekvensdiagram:

![sequence diagram](LSD-Subsystem-SequenceDiagram.png)


#### Frontend

Da vores frontend er lavet i AngularJS fungerer siden som en single-page-application, hvor vi har delt de forskellige undersider op, så de har hver deres view bestående af en .html-fil og en .js-fil. Derudover er der lavet forskellige komponenter som controllerne i .js-filerne har adgang til. komponenterne tæller bl.a. authentication, factory, filter og service.

Alle controllerne benytter sig af vores factory, som er ansvarlig for alt kommunikation med vores backend igennem funktionerne: getStories() og addPost(post). Vores frontend modtager stories når hjemmesiden indlæses, herefter bliver dataen skrevet til browserens localstorage, hvis dette er muligt. I det tilfælde at forbindelsen til vores backend skulle blive brudt, vil brugeren nu være i stand til at bruge en cached version indtil forbindelsen genoprettes. Brugeren vil se en besked under menuen, som beskriver hvorledes det har været muligt at connecte med serveren og/eller det har været muligt at indlæse data fra localstorage, såfremt det er nødvendigt. 

#### Backend

Vores backend er bygget efter BCE-modellen og består af nogle entity-klasser til comment, story og user der benyttes af vores StoryController, som håndterer kommunikationen ned til databasen igennem persistence-laget med PreparedStatements, og op til facaden i boundary-laget, som indeholder vores REST-API der har denne struktur:

- Show latest stories -
GET: /api/stories

- Select story -
GET: /api/stories/view/{id}

- Show comments -
GET: /api/stories/{id}/comments
- Submit story -
POST(Story): /api/stories
- Upvote story -
POST: /api/stories/{id}/upvote
- Downvote story -
POST: /api/stories/{id}/downvote
- Comment on story -
POST(StoryComment): /api/stories/{id}/comment
- Login - 
POST(LoginCredentials): /api/auth/login
- Register -
POST(RegisterCredentials): /api/auth/register

Derudover har vi både i boundary- og control-lagene klasser til at håndtere metrics i forbindelse med prometheus.


#### Database

Logisk data model for vores MySQL database:

![datamodel](datamodel.png)



### 1.4. Software design

#### Frontend
Vi blev ret hurtigt enige om at benytte AngularJS til vores frontend, da vi havde mulighed for at udnytte flere funktionaliteter fra frameworket, som ville spare os for meget tid. Bl.a. databinding og specielt ng-repeat funktionen ville vi kunne udnytte, ved at style og programmere én story eller én comment og derefter påføre den kode og styling til alle elementerne ved at iterere over dem. Samtidig er AngularJS god til at håndtere profiler på en hjemmeside, specielt i forhold til elementer der bør skjules i forhold til om man er logget ind eller ud.

Når vi bruger AngularJS til at kode vores frontend, så laver vi samtidig en SinglePageApplication, hvilket vi ser, som en fordel for brugerne af hjemmesiden, da man kan navigere rundt på hjemmesidens forskellige undersider, uden at skulle indlæse hele siden hver gang.

Vi ønskede at det var muligt for en bruger, at navigere på en cached version af hjemmesiden, hvis brugeren havde besøgt den før, og dermed gemt data om stories og comments i browserens LocalStorage. Derfor udføres der altid et tjek når der hentes eller sendes data med koden:

- `localStorageService.isSupported`

For at sikre at vi kan benytte localStorage hos brugeren, før vi skriver dertil eller læser derfra.  Herefter vil brugerens ændring blive gemt i localStorage ved hjælp af et key/value par, og samtidig sendes ændringen til vores backend igennem vores factory.

Denne funktionalitet betyder at alle brugere der har indlæst hjemmesiden én gang, vil kunne benytte den, selvom vores backend-server skulle gå ned for en stund. 

#### Backend
I forhold til vores backend, aftalte vi i gruppen at vi ønskede at gøre brug af Java som programmeringssprog. Valget faldt på Java, på grund af vi alle sammen i forvejen havde et stort kendskab til sproget, samt vi at tidligere har erfaret at Java har god performance til denne type opgave. Derudover ville vi relativt hurtigt kunne have et REST API kørende, og det samme var gældende for vores database-forbindelse med JDBC. Som tidligere nævnt faldt vores valg af database på MySQL.

**Pattern**
![bce](https://user-images.githubusercontent.com/11289686/34073853-e2e74e18-e2a3-11e7-9433-1b188d3f46ad.png)
> Kilde: http://training-course-material.com/training/UML_Communication_Diagram

Boundary Control Entity, er en variant af MVC modellen. Vi valgte at bruge dette pattern for at uddele ansvaret af opgaver til passende klasser, og for at gøre det nemmere at teste vores klasser og logikken i selve koden.

**Boundary:**
Boundary-laget er grænsen mellem brugergrænseflade og vores ”forretningslogik”. Denne har til formål at isolere API’et fra den resterende del af systemet. Vi valgte at bruge JAX-RS som er Javas API, til RESTful Web Services. 

Udover klasserne til vores REST API, besluttede vi også at have en facade klasse, som skulle fungere som den eneste adgang fra Controller klasserne til vores database.   

**Controller:**
Controller-laget fungerer som et sted til opbevaring af ”hjælper” klasser. Vi valgte at have en stor del af vores logik i dette lag, da det skulle sikre at det blev nemmere at teste koden, sammenlignet med hvis vi havde det hele i Boundary klasserne.   

**Entity:**
Entity-laget ville vi bruge til at opbevare entitets klasser, som skulle bruges til persistering til vores database.
 

#### Database
Vi valgte at bruger en MySQL database til data persistering. Vores valg faldt på en relationel database, da vi mente at den ville havde en bedre performance, (til den forventede mængde af data) end f.eks. Neo4J. Dette havde vi tidligere undersøgt, i vores database fag på 1. semester og kunne med fordel bruge den erfaring vi havde fået derfra. 

Vi besluttede at bruge JDBC (Java Database Connectivity), til at tilgå vores database. Vi valgte at vi ville bruge Java’s Prepared Statements interface til at forespørge i data, samt til opdatering af vores data. Dette valgte vi fordi at Prepared Statement” har en bedre performance end f.eks. ordinære statements, dette skyldes at de kun bliver kompileret én gang, nemlig første gang. Derudover giver det også en bedre sikkerhed, da det sikre at muligheden for ”SQL-injection” elimineres.    


### 1.5. Software implementation

Til implementeringen af vores system valgte vi at følge de samme løsninger som vi havde besluttet under software design fasen.

Vi valgte at implementere vores system på en remote server hos Digital Ocean. Vi valgte løsningen til 10 $ pr. måned, hvilket vi forventede ville kunne opfylde vores behov i forhold til performance på systemet. Den Virtuelle maskine hos Digital Ocean havde følgende ressourcer og operativsystem:
1 GB Memory / 30 GB Disk / FRA1 - Ubuntu 16.04.3 x64   

Det første vi valgte at få sat op var vores MySQL Database. Vi snakkede internt i gruppen om hvordan vi nemmest kunne få en database op og kører som overholdte de krav der var blevet aftalt tidligere. Vi valgte derfor at se bort fra ”vote” tabellen, da vi mente denne del med fordel kunne undværes til at starte med. Dette valgte vi for at gøre det nemmere for os selv, hurtigst muligt at have et system oppe at kører, som ville kunne modtage og håndtere den data der blev sendt i requests af simulatoren.

Da vi ville installere MySQL på vores remote server, mødte vi de første problemer. Vores hostede maskine havde ikke nok hukommelse til at installere MySQL. Dette løste vi ved på serveren at lave en ”Swap-fil”. Dette er kort fortalt et område på harddisken, der er udpeget som et sted, hvor operativsystemet midlertidigt kan lagre data, som den ikke længere kan holde i hukommelsen. Dybest set giver det mulighed for at øge mængden af informationer, som serveren kan beholde i sin "hukommelse". Pladsen på harddisken vil blive brugt, når der ikke længere er tilstrækkelig plads i RAM. Vi lavede derfor en swap-fil på 1 GB, hvilket løste problemet med at installere MySQL. Vi mødte også problemer med adgang til databasen fra vores Java applikation, men dette blev hurtigt løst via. simpel ”SQL sikkerhed og privilegie” konfiguration.

I forbindelse med implementering af vores Java backend gik alt som det skulle, og vi fik sat vores continuous integration chain op at kører, med Github, Jenkins, Docker og Maven, samt deployement til Digital Ocean. Desværre mødte vi på samme måde som ved installeringen af MySQL tilsvarende hukommelses problemer med Java, efter noget tid i drift. Vi opdagede at vores system pludselig var gået ned og vi kunne se i system log filen at dette skyldtes at Java var løbet tør for hukommelse. Vi måtte derfor endnu engang lave en swap-fil, denne gang på 4 GB i stedet for 1 GB. Dette løste problemerne med hukommelsen og Java.

Vi blev lidt længere tid i drift, dog orienteret om at vores system var ” virkelig langsomt med at håndtere beskeder som bliver sent ud fra simulatoren”. Vi var på forhånd opmærksomme på at vores server på Digital Ocean, i perioder var presset på hukommelse, men vi besluttede at undersøge vores backend kode i stedet for at opgradere til en dyrere løsning. Vi mente vi at der måtte være steder i selve koden som kunne optimeres, og dermed måden vi håndtere hvert request. Vi lavede derfor lavet nogle test cases i JUnit, som kunne vise os, hvor hurtigt hvert request blev behandlet. Den første test lavede vi på en lokal udgave af det system vi havde i drift. Den viste at det tog 0.9 sekunder for hvert request, før der blev sendt et response tilbage. Vi fjernede derefter al det kode vi mente var overflødigt/unødvendigt, og ændrede i måden hvor på vi håndterede brugernavn og password i hvert request. Dette medførte at det efterfølgende tog 0.45 sekund, per request. Optimalt set burde vi også havde undersøgt muligheden for at kører med flere tråde eller skalere vores service, og på den måde opnå en bedre performance, men grundet tidspres og prioritering 

## 2. Maintenance and SLA status

### 2.1. Hand-over ###
Den 6. november modtog vi et link til en pdf på den gruppe vi skulle agerere operator for. Pdf’en indeholder det mest nødvendige information omkring systemet. I starten står der hvilken ip adresse systemet befinder sig på, efterfølgende får vi lidt flere informationer omkring hvordan det hele er sat op i forhold til servere og virtuelle maskiner.
Der står også vi kan få adgang ind på serveren hvis vi ønsker, og vi bare skal kontakte dem så skal de nok give os en forbindelse. der er også lavet et diagram der viser dataflowet i systemet. Der er også linket til et andet dokument der udførligt beskriver backenden, i forhold til hvilke kald der er mulige at udføre, hvilke routes man skal bruge, om det er GET, PUT eller POST, hvad der forventes at blive sendt med i requested og hvad man kan forvente at få tilbage, både ved et succesfuld request og et med fejl. Det eneste man kunne sætte en finger på, er at der ikke er skrevet at man skal kalde på port 8080, men det gættede vi os hurtigt frem til, da de havde skrevet at backenden var skrevet i Java.
Til sidst er der nævnt hvordan vi skal indrapportere bugs i deres system.

Så overordnet set har vi været yderst tilfredse med den dokumentation der er blevet sendt til os, den har været godt gennemarbejdet, og det virker velovervejet det der er skrevet.

### 2.2. Service-level agreement ###
  
I forbindelse med gruppe f er vi blevet enige om en SLA som inderholder følgende punkter:

* En oppetid på 99%. 
* Response time skal maks være på 10 sekunder. 

Disse punkter har fået et lille afsnit hver nedenfor hvor der vil blive nærmere uddybet hvordan disse krav skal fortolkes.

#### Oppetid ####
Vi er blevet enige med gruppe f om at deres system skal have en oppetid på 99% eller højere. Oppetiden skal beregnes ved at sende request til serveren til API’ets status funktion, som er lavet til at tjekke om serveren er i live. Ud fra det samlet antal af kald og antallet af succes kald, måles serverens oppetid.

Dog vil gruppen ikke blive holdt ansvarlige for en faldende oppetid i tilfælde af begivenheder der er ude af deres kontrol, dette inkludere bl.a. at deres hosting firma bliver angrebet af hackere eller udsat for strømsvigt.

#### Responstid #### 
Vi har aftalt at systemet ikke må være mere end 10 sekunder om at svare, denne tid er fra serveren modtager et request til den sender et response retur, dette vil betyde at gruppen ikke vil blive holdt ansvarlig for en eventuel ekstraordinær dårlig internetforbindelse fra slutbrugerens side af.
Tiden vil blive målt som den gennemsnitlige request tid, for det samlede antal request der sendes afsted til serveren. 

### 2.3. Maintenance and reliability

Under forløbet har vi kigget på gruppe f’s system. 
Vi har prøvet både at benytte systemet som en almindelig bruger, ved at bruge frontenden, derudover har vi også prøvet at kalde direkte til apiet, dette har vi gjort ved at benytte postman.

Ved almindelig brug har alt bare været som det skulle være. 
Vi har også prøvet bevidst at sende forkerte data afsted igennem postman for at se om vi kunne lave noget der ville få systemet til at breake. 
Vi har også prøvet at lave sql injections fra deres client, for at se om vi ville være i stand til at udføre nogle kald på databasen som vi ikke ellers vi være i stand til.

Det har dog ikke lykkedes for os at finde noget på deres system, der har været værd at indberette, Og vi kan derfor kun sige at gruppens system har været yderst pålideligt.  

## 3. Discussion

## 3.1. Technical discussion
Udfra de krav der blev stillet, havde vi designet et system og vi har forsøgt at udvikle system ud fra dette. På trods af udfordringer på vejen, har vi nogenlunde fulgt det originale design. Det har gennem en stor del af projektet været lidt kaotisk, da vi ikke har fået brugt Trello så meget som vi originalt aftalte, men gennem kommunikation har vi fået løst de fleste problemer. Det har overordnet været fint nok. 

Vi har kun nået at implementere omkring halvdelen af vores use cases. Nogle blev fravalgt da de ikke var en del af minimumskravene, for at spare tid.

Vores kommunikation har været god og vi har alle været med til at udvikle. Vores valg af database, udviklingssprog og andre teknologier har virket efter hensigten, for det meste.

Selve programmet har ikke skabt voldsomme problemer, men den initielle opsætning var et problem da vi ikke kunne tilgå serveren med Jenkins. Vi fik det dog løst med en lokal installation, selvom dette ikke er helt optimalt. 

Det er heller ikke lykkedes os at implementere logging/ELK stacken ordenligt, da vi har haft problemer med installation og implementering i koden. 

Vi har desværre ikke været gode nok til at monitor den anden gruppes system. Det skyldes bl.a. at vi har været optaget af vores eget system, da vores eget ikke har kørt optimalt. Vi har ikke selv modtaget bug issues, udover fra Helge. Vi har forsøgt så vidt muligt at leve op til SLA, men på grund af sent opdagede fejl, har vi først senere hen komme op på et nogenlunde niveau. 


## 3.2. Group work reflection & Lessons learned
