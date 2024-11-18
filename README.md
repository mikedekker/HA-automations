Dit is een automatisering voor het laden van een elektrische auto aangestuurd door Home Assistant.

De automatisering "Laden - Start bepalen" zorgt er voor dat er bij het aansluiten van je auto op de kabel de vraag op je mobiel komt hoe je wil laden. Wil je dit zo snel mogelijk, voor 6 uur de volgende ochtend of binnen 24 uur?
De automatisering zorgt er voor dat er op de goedkoopste tijden geladen zal worden.

Een voorbeeld van wat er gebeurt.
  Een melding komt op je telefoon met de vraag of je zo snel mogelijk, voor 6 uur of binnen 24 uur wil laden. Je kiest voor 6 uur.
  De sensor voor de batterijpercentage van de auto geeft aan dat er nog 40% in de batterij aanwezig is.
  Aan de hand van snelheid van de laadpaal en maximale capaciteit van de accu bepaalt het systeem hoeveel uur er nodig is om te laden. Als voorbeeld is er 4 uur nodig om te laden.
  Aan de hand van data van de Nordpol integratie verzamelt het alle prijzen tot 6 uur de volgende ochtend en bepaalt de goedkoopste 4 uur om te laden. Dat zijn 23:00, 1:00, 3:00 en 4:00 uur.
  De automatisering kijkt aan het eind of het op dit moment een uur is welke goedkoop is.
    Als het 23:00 uur is zal de automatisering de laadpaal inschakelen
    Als het 22:00 uur is zal de automatisering de laadpaal uitschakelen en wachten tot een uur dat het wel goedkoop is

Nadat het eerste initiele stuk is afgelopen dient er ook een automatisering te zijn die elk uur kijkt of de laadpaal in- of uitgeschakeld moet worden. Dit doe je met de automatisering "Laden - Periodieke controle".
Deze automatisering controleert elk uur of het een goedkoop uur is en schakelt hier de laadpaal op.

Welke integraties zijn er gebruikt:
Tesla integratie
    Om de batterij percentage van de auto uit lezen
  Alfen laadpaal integratie
    Om de status van de kabel uit te lezen en het laden in en uit te schakelen
  Nordpol integratie
    Voor het ophalen van de actuele stroomprijzen van een dynamisch contract

Welke helpers moet je aanmaken?
  input_number.laden_klaar
    minimumwaarde: -1
    maximumwaarde: 23
  input_text.goedkopelaadtijden
    minimumlengte: 0
    maximumlengte: 254

Wat moet je persoonlijk aanpassen in de automatisering?
  sensor.laadpaal
    Dit is de sensor die de status van je laadpaal aangeeft. Dus charging of available
  sensor.tesla_battery_level
    Dit is de sensor die het batterij percentage van de auto aangeeft
  notify.mobile_app_iphone
    Dit is het device waar je de meldingen heen wil sturen
  autocapacity: 60
    Pas het getal 60 aan naar de kWh capaciteit van je auto
  chargercapacity: 11
    Pas dit getal aan naar het maximale laadvermogen van je laadpaal of auto
  sensor.nordpool_kwh_nl_eur_2_11_031
    Pas dit aan naar de Nordpol integratie sensor
  number.laadpaal_max_station_current
    Pas dit aan naar de sensor die instelt met hoeveel Ampere de laadpaal kan laden
