# Integratieopdracht DevOps
`voorzie badge hier (zie opgave)`

## Inleiding
Het bedrijf OpsDev heeft met argusogen de lessen Devops op 2TIN meegevolgd en is zelf aan de slag gegaan aan een eigen versie van de calculator app die we gebruikt hebben tijdens de lessen. Je zou kunnen stellen dat er enkele gelijkenissen zijn tussen de app gebruikt tijdens de les en die van het bedrijf. Naast het ‘op een correcte manier kopiëren van applicaties’ is het bedrijf OpsDev ook vies van Jenkins en (lokaal gehoste) virtuele machines.

Jij start als junior-collega in het bedrijf OpsDev en bent verantwoordelijke voor het opzetten van een systeem waarbij je CI & CD toepast. Zoals aangegeven mag er geen jenkins of virtuele machine gebruikt worden. Op aangeven van Kevin, Head of Operations (Je baas), ga je je verdiepen in Github actions en heroku. De code van hun calculator applicatie is terug te vinden in deze repository.

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip")
_(a) Inventariseer kort in oplossing.md waarvoor github actions en heroku gebruikt worden. Wie zit er achter deze toepassingen? Wat is het doel?_

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip")
_Maak een account aan op [heroku](http://heroku.com)._

# Let's get started!
OpsDev hecht veel waarde aan kwaliteit & feedback. Een CI/CD pipeline is dan ook een must-have voor het bedrijf. Helaas heeft in-house niemand buiten jijzelf de kennis om CI/CD pipelines te bouwen.

Voor de continious integration fase van het bouwen van de applicatie zal je gebruik maken van Github actions.  Je zal merken dat hier verschillen in zitten ten opzichte van jenkins. 

Github actions heeft meteen een zeer goede integratie met het Github ecosysteem. Dit is iets waar je perfect gebruik van kan maken. Je zal de guidelines van de documentatie strict  moeten volgen om een werkend product te krijgen.

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip") _Begin alvast met het volgende van de quickstart guide op [deze link](https://docs.github.com/en/actions/quickstart) en pas deze toe op deze repository._

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip")
_(b) Na het verkennen van Github Actions zal je merken dat er gebruikt gemaakt wordt van yaml files. Wat voor soort files zijn dit? hoe zijn die opgebouwd? Hoe zit een yaml syntax/structuur eruit? Documenteer in oplossing.md_

# CI workflow
Het eerste doel van onze CI "workflow", zo noemen we een pipeline in Github Actions, is dat de github repository code binnengetrokken wordt. Je zal merken dat dit op zich vrij eenvoudig gaat. Voorziek een nieuwe workflow met als naam `<groepsnaam>-OpsDev-CI` die draait op een ubuntu systeem met daarin een stap die de code van de repository binnentrekt. De nodige info hiervoor kan je terugvinden in de quickstart guide die hierboven gelinkt was.

De volgende stap is het voorzien van triggers voor de workflow. Wanneer wordt de workflow uitgevoerd? Bekijk [deze documentatie](https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows). En zorg ervoor dat de pipeline handmatig gestart kan worden & dat de pipeline ook automatisch runt bij een nieuwe push naar de main branch.

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip")
_Start de pipeline handmatig om te testen of je workflow werkt. Bekijk de output in de actions tab van je repository_

Hierna willen we graag de unittesten van de applicatie runnen. hiervoor hebben we eerst de dependencies(=node_modules) van de applicatie nodig. Deze kan je installeren via het commando `npm install` dat je in de pipeline dient uit te voeren. Hiervoor heb je uiteraard nodeJS nodig. Lees [deze documentatie](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs-or-python) door en voorzie een stap die nodeJS integreert in je workflow. Daarna voorzie je ook een stap die de dependencies installeert. Tenslotte voorzie je een stap die de unittesten uitvoert.

Het rapport willen we graag archiveren als artifact van de build poging. Voorzie een stap die dit doet. Informatie hierover kan je [hier](https://docs.github.com/en/actions/advanced-guides/storing-workflow-data-as-artifacts) terugvinden.

Feedback is belangrijk. Het is mogelijk om een badge toe te voegen aan de `README.MD` die de status van de laatste build poging weergeeft. Voorzie dit a.d.h.v. [deze documentatie](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge).

# Integratie pull requests
Zorg ervoor dat de CI workflow ook uitgevoerd wordt bij het maken van een pull request. 
Test dit uit door nieuwe feature uit te werken aan de hand van de Github flow. Je werkt de feature uit om machtsberekeningen te maken. Maak na het afwerken van de feature een Pull request aan voor de merge. Controleer of de workflow ook effectief uitgevoerd wordt. Waar kan je dit terugvinden in de pull request?

# Continious deployment
Voorzie een nieuwe workflow in je repository met als naam '`<groepsnaam>-OpsDev-CD`. Deze workflow wordt enkel manueel gestart. Het doel van deze workflow is dat er een deployment uitgevoerd zal worden naar Heroku (Je baas is enorme fan van heroku, hij heeft daar namelijk verschillende tshirts van).

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip")
_(f) Wat is heroku juist? Waarvoor kunnen we dat gebruiken?_

Voor de opzet van je Heroku app helpen we je graag verder:

*   Log in met je aangemaakte account op Heroku. Je zal merken dat heroku ook een free-tier heeft waar je mee aan de slag kan.

*   Maak een nieuwe app aan. De naam van de app is best dezelfde als die van je repository. Je hoeft deze niet toe te voegen aan een pipeline (Heroku heeft ook zijn eigen pipeline systeem & zijn eigen versiebeheersysteem).

*   Tenslotte moet je een API key genereren in de settings van je profiel. Onder het tabblad account kan je de API key terugvinden.

Voor een deployment naar heroku is het handig om een Dockerfile te voorzien in je applicatie. Op die manier gaat heroku heel veel voor ons afhandelen.

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip")
_Voorzie een `Dockerfile` in de root van deze repository die de nodeJS opstart (denk ook aan de `npm install` in de container)_

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip")
_Na het aanmaken van de Dockerfile kan je starten met de deployment workflow. Bekijk hiervoor [deze](https://github.com/marketplace/actions/deploy-to-heroku) documentatie._

**!Let op: de API key van Heroku mag niet zichtbaar zijn in yml file!**

_tip: gebruik hiervoor in [Github secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)_


Tenslotte willen we bij elke deployment een bericht krijgen in onze discord server. Bouw zelf een nieuwe discord server (of gebruik een bestaande) en voorzie discord alerts. Documentatie hiervoor kan je [hier](https://github.com/marketplace/actions/actions-for-discord) terugvinden. Ook hier willen we niet dat de webhook url zichtbaar is in de yml file.

![alt_text](https://i.imgur.com/5STVnt2.png "image_tooltip")
_(g) Waarom maken we voor het gebruik van de API key & webhook URL gebruik van secrets (ook wel environment variabelen genoemd)? Wat is daar het voordeel van? Zijn er nog andere manieren waarop je dit kon doen?_

# Extra challenge (optioneel)
In plaats van een deployment naar heroku ga je een docker image builden en deze opslaan als github package gelinkt aan deze repository. Volgende [documentatie](https://docs.github.com/en/actions/publishing-packages/publishing-docker-images) kan je op weg helpen.

# Deliverable
- Een CI workflow
- Een status badge in de `README.md` file
- Een CD workflow
- De link naar je gedeployde applicatie op heroku bovenaan in `oplossing.md`





