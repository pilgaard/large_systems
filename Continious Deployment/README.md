# Continious Deployment

## Link to MVP:
http://46.101.111.112/


## Brief description of the CD technology

Vi har til vores projekt valgt at bruge følgende værktøjer til CI/CD:

- Git: 
<br>
Bruger vi til version control system

- Github:
<br>
Bruger vi til at hoste vores kode

- Jenkins: 
<br>
Bruger vi til bygge server

- Maven:
<br>
Bruger vi til at bygge vores projekt

- Vagrant:
<br>
Bruger vi til setup og configurering af virtual maskiner (Både lokalt og på digital Ocean)

- Digital Ocean:
<br>
Bruger vi som Cloud server


## Setup and config

Vi har som nævnt valgt at bruge Jenkins som bygge server. Til vores Backend har vi valgt at udvikle i Java og Maven bruger vi til at bygge projektet til en JAR fil.
<br>
Jenkins peger på vores GitHub repository, så når vi push'er til Git, vil Jenkins automatisk bygge projektet   
