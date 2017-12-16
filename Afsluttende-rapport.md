# Large system development report # 
### 2.1. Hand-over ###
Den 6. november modtog vi et link til en pdf på den gruppe vi skulle agerere operator for. Pdf’en indeholder det mest nødvendige information omkring systemet. I starten står der hvilken ip adresse systemet befinder sig på, efterfølgende får vi lidt flere informationer omkring hvordan det hele er sat op i forhold til servere og virtuelle maskiner.
Der står også vi kan få adgang ind på serveren hvis vi ønsker, og vi bare skal kontakte dem så skal de nok give os en forbindelse. der er også lavet et diagram der viser dataflowet i systemet. Der er også linket til et andet dokument der udførligt beskriver backenden, i forhold til hvilke kald der er mulige at udføre, hvilke routes man skal bruge, om det er GET, PUT eller POST, hvad der forventes at blive sendt med i requested og hvad man kan forvente at få tilbage, både ved et succesfuld request og et med fejl. Det eneste man kunne sætte en finger på, er at der ikke er skrevet at man skal kalde på port 8080, men det gættede vi os hurtigt frem til, da de havde skrevet at backenden var skrevet i Java.
Til sidst er der nævnt hvordan vi skal indrapportere bugs i deres system.

Så overordnet set har vi været yderst tilfredse med den dokumentation der er blevet sendt til os, den har været godt gennemarbejdet, og det virker velovervejet det der er skrevet.

### 2.2. Service-level agreement ###
  
Vores SLA inderholder følgende:
* En oppe tid på 99%. Måles på request mod serveren.
* Response time skal maks være på 10 sekunder. Måles som gennemsnitlig request time for de request der laves på serveren. 

