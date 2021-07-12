# Relatie zibs en KIK-V ontologie
In deze notitie wordt behandeld wat de relatie is tussen Zorg Informatie Bouwstenen (zibs) en de KIK-V ontologie; het equivalent van zibs binnen het programma KIK-V. Het programma KIK-V is veel breder dan alleen de ontologie. Dit vormt slechts één element in de keten van informatie-uitwisseling. Dit document gaat alleen over de ontologie.

# Zorg Informatie Bouwstenen
Elke zib beschrijft een (klinisch) concept, dat meerdere gegevens in zich herbergt met een afgesproken inhoud, structuur en onderlinge relaties (bron: https://informatiestandaarden.nictiz.nl/wiki/Zib:Zib_Centrum_FAQ)
Een zib is een model in de informatielaag, dat definieert op welke manier (wat betreft codering, meeteenheid, attributen enz.) een gegevenselement vastgelegd kan worden in een systeem binnen een proces, om interoperabiliteit op semantisch niveau mogelijk te maken, als dat gegevenselement ook in andere processen (en bijbehorende systemen) beschikbaar moet zijn (zoals allergie, huidige medicatie of actuele zwangerschap). (bron: Architectuurdocument volume 1)
## Overeenkomsten
* Zibs zijn gericht op het hergebruik van vastgelegde informatie en hebben hier een wezenlijke overeenkomst met de doelstellingen van KIK-V.
* Een zib richt zich op de betekenis van informatie en niet op het technische formaat ervan. Hetzelfde geldt voor de ontologie binnen KIK-V. Beide willen nadrukkelijk de technische implementatie (bij een zorgaanbieder) niet voorschrijven.
* Zibs maken gebruik van bestaande standaarden zoals HL7 en SNOMED CT. Ook binnen de ontologie van KIK-V wordt zoveel mogelijk gebruik gemaakt van bestaaande standaarden.
* Zowel de zibs als een ontologie zijn semantische modellen die betekenis vastleggen.
## Verschillen
* De ontologie binnen KIK-V is machine-leesbaar. Dat wil zeggen dat de (semantische) betekenis die in de ontologie vastligt door een machine gebruikt kan worden om conclusies te trekken uit die gegevens.
* De scope van de ontologie is breder dan het zorgproces. Er wordt bijvoorbeeld ook gekeken naar bedrijfsvoering, personeel en financiën.

Een aantal technische verschillend, bijvoorbeeld:
* Binnen Zibs wordt een concept als Adresgegevens specifiek gemaakt. NL-CM:0.1.4 = adresgegevens van de patient, NL-CM:3.1.5 = adresgegeves van de contactpersoon, NL-CM:17.1.7 = adresgegevens van van de zorgverlener. Terwijl het concept adresgegevens wel steeds dezelfde definitie houdt. Binnen de ontologie wordt hier dan één relatie voor gebruikt.
* Binnen de ontologie wordt gewerkt met RDF ([Resource Descriptive Framework](https://www.w3.org/TR/rdf11-concepts/), een W3C standaard). Hierbinnen krijgen alle te beschrijven resources een unieke identifier in de vorm van een URL. Een woonplaats als Amsterdam wordt dan gerepresenteerd als http://bag.basisregistraties.overheid.nl/bag/id/woonplaats/3594, in plaats van "Amsterdam".

# Hergebruik zibs binnen de ontologie
Omdat de zibs uitgaan van semantische beschrijving van concepten, is deze informatie in principe bruikbaar bij het opstellen van de ontologie. Doordat de ontologie in een machine-leesbare taal wordt opgesteld: de Web Ontology Language (OWL), zal deze altijd 'vertaald' moeten worden.

Tot nu toe zijn de zibs impliciet gebruikt, net zoals allerlei standaarden zijn gebruikt voor het opstellen van de ontologie. Voor het opstellen van het zorg-inhoudelijke deel van de ontologie is het de bedoeling:
* expliciet de zibs te hergebruiken als basis voor de relevante concepten
* de concepten in de ontologie te 'annoteren' om aan te geven in hoeverre concepten met elkaar overeenkomen via het Simple Knowledge Organization System ([SKOS](https://www.w3.org/TR/2009/NOTE-skos-primer-20090818/)). Voor ieder concept is dan bijvoorbeeld te zien of ze precies overeenkomen (skos:exactMatch) of grotendeels overeenkomst (skos:closeMatch).

De relatie tussen zibs en de ontologie ligt daarmee expliciet vast ín de ontologie zelf. Dat geeft de mogelijkheid om middels een query al deze relaties te publiceren zodat deze op één plek eenduidig beschikbaar zijn, zonder dat de relaties handmatig 'opgezocht' hoeven te worden in de ontologie.

# Voorbeeld (technisch)

## Voorbeeld: adres
Adressen worden vooralsnog niet gebruikt voor de berekening van indicatoren, maar het concept is wel aanwezig in de ontologie om metdata van zorgverleners te kunnen opnemen. 
### Definitie
Zib (Adresgegevens): Adresgegevens bevatten de gegevens waar een persoon (tijdelijk of vast) woont of waar een gebouw zich bevindt.

Ontologie ([Adres](http://purl.org/ozo/vph-pers#Adres)): Een adres is een door het bevoegde gemeentelijke orgaan aan een verblijfsobject, een standplaats of een ligplaats toegekende benaming, bestaande uit een combinatie van de naam van een openbare ruimte, een nummeraanduiding en de naam van een woonplaats. (o.b.v. Kadaster definitie)

Voor sommige onderdelen is de vertaling makkelijk. In dit geval sluit de definitie van adres(gegevens) elkaar niet uit. Dat geldt bijvoorbeeld voor het onderdeel Huisnummer (Zib) / [huisnummer](http://purl.org/ozo/vph-pers#heeftHuisnummer) (ontologie). In beide gevallen gaat het over een data-element dat wordt opgeslagen als een nummer.

Echter voor het onderdeel Woonplaats (Zib) is de vertaling wat complexer. Binnen de Zib is Woonplaats een string met tekst, bijvoorbeeld: "Amsterdam". In de ontologie is het equivalent van Woonplaats een concept. De data voor de 'instantie' Amsterdam zou er als volgt uizien: http://bag.basisregistraties.overheid.nl/bag/id/woonplaats/3594

Dit voorbeeld is bedoeld om te illustreren dat direct vertaling van een zib naar de ontologie niet altijd mogelijk is.

Het is wel mogelijk om aan te geven dat er een relatie is tussen de onderdelen en wat de aard van die relatie is. Binnen de ontologie gebruiken we dit mechanisme bijvoorbeeld om aan te duiden dat [huisnummer (KIK-V)](http://purl.org/ozo/vph-pers#heeftHuisnummer) een exacte overeenkomst is met [huisnummer (Kadaster)](http://bag.basisregistraties.overheid.nl/def/bag#huisnummer). Op dezelfde manier zouden we kunnen duiden dat het een exacte match is met [huisnummer (Zib)](https://zibs.nl/wiki/Adresgegevens-v1.1(2020NL)).

In het geval van Woonplaats zou de relatie geen exacte match, maar een 'close match' moeten zijn.