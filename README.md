# hacker_news

## Introduction
- Purpose of the System
	- Formålet er at bygge en hjemmeside, hvor registrerede brugere kan lave indlæg, der både kan ses, kommenteres og vurderes af andre brugere. De enkelte kommentarer på indlæg kan også vurderes af andre brugere. Dette vil resulterer i et miljø, hvor brugere kan dele deres oplevelser eller interessante nyheder med andre brugere, hvilket kan lede til mange forskellige slags interaktioner imellem hjemmesidens brugere.
	- Systemet kan sammenlignes med HackerNews og Reddit (se References).
- Scope of the System

- Objectives and success criteria of the project
	- Objecives:
		- At anvende en Agile udviklingsmetode. Dette vil effektiviserer udviklingen af systemet.
	- Success criteria:
		- Systemet vil have en meget høj oppetid, og at der ikke går noget data tabt.
		- Alt data bliver gemt i en database.
		- En hjemmeside hvor alle indlæg kan ses, kommenteres og reageres på.
		- Brugere kan:
			- Registrere sig i systemet med både Username og Password.
			- Både logge ind og ud af systemet.
			- Lave indlæg.
			- Kommenterer på indlæg og andre brugeres kommentarer.
			- Reagerer på andre brugeres indlæg og kommentarer, ved enten at Up eller Down vote.
			- Modtage Karma point, baseret på hvor mange Up og Down votes de får.
				
	- Definitions, acronyms and abbreviations
		- Karma point: Karma point er summen af alle Up votes en brugers indlæg eller kommentarer har fået, minus summen alle Down votes brugerens indlæg eller kommentarer har fået.
		- Indlæg: Et indlæg kan bestå af billeder, tekst, links, gifs, videoer mm. 
		-  
	- References
		- Reddit: https://www.reddit.com/
		- HackerNews: https://news.ycombinator.com/ 
		- Både Reddit og HackerNews er sociale nyhedshjemmesider, hvor brugere kan lave indlæg, der kan kommenteres og reageres
		på af andre registerede brugere.
	- Overview

## Current system
Der er som udgangspunkt intet nuværende eksitrende system. Det kommende system skal dog efterligne det eksisterende site "Hacker News".

## Proposed system

### Overview

Systemet skal som udgangspunkt fungere som et socialt nyhedswebsite, med fokus på computervidenskab og iværksætteri. Målet med udviklingen af systemet, er at have et website med en funktionalitet der minder om Reddit og mere specifikt være en efterligning af "Hacker News" (https://news.ycombinator.com/).

Systemet skal kunne håndtere at brugere kan registrere sig på siden og tilføje nyheder og historier, og kommentere på eksisterende indhold. Derudover skal brugere af websitet kunne up- og down-vote på historier eller kommentarer, alt efter om brugeren mener at indholdet bidrager med noget positivt eller negativt.     


### Functional requirements

## User Stories

| **Id** | **User Story** | **Id** | **User Story** |
| --- | --- | --- | --- |
| **1** | A user must be able to read stories without logging in | **2** | A user must be able to register a new account |
| **3** | A user must be able to retrieve a new password for his/her account. | **4** | A user must be able to log in to his/her account |
|   | **After successful login** |   |   |
| **5** | A user must be able to submit new stories. | **6** | A user must be able to edit his/her submitted stories. |
| **7** | A user must be able to view a list of submitted stories | **8** | A user must be able to delete his/her stories |
| **9** | A user must be able to view all comments submitted to a story | **10** | A user must be able to submit a comment to a story |
| **11** | A user must be able to submit a comment to a comment | **12** | A user must be able to edit his/her submitted comments |
| **13** | A user must be able to delete his/her comments | **14** | A user must be able to view a list of his/her submitted comments |
| **15** | A user must be able to edit his/her profile | **16** | A user must be able to edit the email assigned to his/her profile |
| **17** | A user must be able to mark stories as  favorites | **18** | A user must be able to mark comments as favorites |
| **19** | A user must be able to view a list of all favorite entities | **20** | A user must be able to remove entities from his/her list of favorites |
| **21** | A user must be able to switch between sub-pages of different categories. | **22** |   |
| **23** | A user must be able to flag stories as spam | **24** | A user must be able to flag comments as spam |
| **25** | A user must be able to upvote stories | **26** | A user must be able to downvote stories when they have 500+ karma |
| **27** | A user must be able to upvote comments | **28** | Users must be able to downvote comments when they have 500+ karma |
| **29A** | A user must be able to view his/her amount of karma points | **29B** | Karma points must be calculated by (upvotes - downvotes) |
| **30** | A User must be able to log out | **31** |   |
| **32** |   | **33** |   |


### Nonfunctional requirements
  - Usability
     - Systemet skal have et REST API som gør det muligt for et simulator program at publicere og kommentere.
     - REST API’et skal også kunne fortælle hvilken stadie systemet er i, fx om det er kørende eller ved at opdatere.
     - API’et skal også kunne fortælle hvem der sidst har skrevet et indlæg eller en kommentar.
  - Reliability 
    - Systemet skal have en oppetid på mere end 95%.
    - Systemet må ikke miste noget af det data som bliver modtaget fra simulator programmet.
    - Der skal være en buffering mekanisme som kan gemme indkommende indhold imens systemet er nede og publicere det når systemet kommer online igen.
  - Performance 
  - Supportability 
  - Implementation 
    - Systemet skal deles op i en frontend og en backend.
    - Frontenden skal vise artiklerne og kommentarerne.
    - frontenden skal også kunne tage imod nye indlæg.
    - backenden skal modtage dataen fra frontenden og sørger for at gemme den.
    - backenden skal også give frontenden alt den data som frontenden har brug for.
    - alt data skal gemmes i en database.
  - Interface
  - Packaging
  - Legal
  
### System models

## Glossary
