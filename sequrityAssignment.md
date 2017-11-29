#Assignment

## Asset definition

- Vores Database
Datasen indeholder alt vores data, og uden den har vi ikke noget produkt

- vores server
Serveren har kontakt til vores Database, som også er et asset defor skal vi beskytte serveren så eventuelle hackere ikke kan tilgå Datasen herfra.

- vores frontend
Frontenden er den der gør at brugerne let kan læse og skrive til systemet


##Threat modelling
Threats
- hackere som kunne finde på at lægge vores server ned
- hackere som kunne finde på at slette data fra vores database
- mulighed for at poste stories til systemet uden at være logget ind
- brute force angreb

Assets
- Database
- server

Vulnerabilities
- Brugernavn og password ligger tilgængeligt på github hvilket gør det let at få adgang til hele databasen
- vores simulator Endpoint er tilgængeligt for alle, det burde være begrænset til at kun helges ip kunne få adgang
-  serveren ligger hos digital-ocean, dette gør at vi ikke har fuld kontrol over vores system
- vi har ingen begrænsninger sat op på hvor mange gange man kan prøve at logge ind i vores frontend hvilket gør at det vil være muligt at brute force sig ind i systemet