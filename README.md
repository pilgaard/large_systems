# hacker_news

## Introduction

## Current system
Der er som udgangspunkt intet nuværende eksitrende system. Det kommende system skal dog efterligne det eksisterende site "Hacker News".

## Proposed system

### Overview

Systemet skal som udgangspunkt fungere som et socialt nyhedswebsite, og målet er at have et system med en funktionalitet der minder om Reddit og mere specifikt være en efterligning af "Hacker News" (https://news.ycombinator.com/).

Systemet skal kunne håndtere at brugere kan registrere sig på siden og tilføje nyheder og historier, og kommentere på eksisterende indhold. Derudover skal brugere af websitet kunne up- og down-vote på historier eller kommentarer, alt efter om brugeren mener at indholdet bidrager med noget positivt eller negativt.     


### Functional requirements

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
