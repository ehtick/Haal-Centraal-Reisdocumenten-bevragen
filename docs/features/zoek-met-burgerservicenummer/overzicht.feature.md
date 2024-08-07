---
layout: page-with-side-nav
title: Zoek met burgerservicenummer
---
#language: nl  


# Functionaliteit: Zoek met burgerservicenummer


## Rule: voor het zoeken van reisdocumenten van een persoon moet het burgerservicenummer worden opgegeven


### Scenario: de gezochte persoon heeft één reisdocument

* __Gegeven__ de persoon met burgerservicenummer '000000152' heeft een 'reisdocument' met de volgende gegevens

  | naam                                        | waarde    |
  |---------------------------------------------|-----------|
  | soort reisdocument (35.10)                  | PN        |
  | nummer reisdocument (35.20)                 | NE3663258 |
  | datum einde geldigheid reisdocument (35.50) | 20240506  |
* __En__ de persoon heeft de volgende 'verblijfplaats' gegevens

  | gemeente van inschrijving (09.10) |
  |-----------------------------------|
  | 0800                              |
* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 000000152                  |
  | fields              | reisdocumentnummer         |
* __Dan__ heeft de response een 'reisdocument' met de volgende gegevens

  | naam               | waarde    |
  |--------------------|-----------|
  | reisdocumentnummer | NE3663258 |

### Scenario: de gezochte persoon heeft meerdere reisdocumenten

* __Gegeven__ de persoon met burgerservicenummer '000000152' heeft een 'reisdocument' met de volgende gegevens

  | naam                                        | waarde    |
  |---------------------------------------------|-----------|
  | soort reisdocument (35.10)                  | PN        |
  | nummer reisdocument (35.20)                 | NE3663258 |
  | datum einde geldigheid reisdocument (35.50) | 20240506  |
* __En__ de persoon heeft een 'reisdocument' met de volgende gegevens

  | naam                                        | waarde    |
  |---------------------------------------------|-----------|
  | soort reisdocument (35.10)                  | NI        |
  | nummer reisdocument (35.20)                 | ID82046A7 |
  | datum einde geldigheid reisdocument (35.50) | 20281103  |
* __En__ de persoon heeft de volgende 'verblijfplaats' gegevens

  | gemeente van inschrijving (09.10) |
  |-----------------------------------|
  | 0800                              |
* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 000000152                  |
  | fields              | reisdocumentnummer         |
* __Dan__ heeft de response een 'reisdocument' met de volgende gegevens

  | naam               | waarde    |
  |--------------------|-----------|
  | reisdocumentnummer | NE3663258 |
* __En__ heeft de response een 'reisdocument' met de volgende gegevens

  | naam               | waarde    |
  |--------------------|-----------|
  | reisdocumentnummer | ID82046A7 |

### Scenario: de gezochte persoon heeft geen reisdocument

* __Gegeven__ de persoon met burgerservicenummer '000000152' heeft de volgende 'verblijfplaats' gegevens

  | gemeente van inschrijving (09.10) |
  |-----------------------------------|
  | 0800                              |
* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 987654321                  |
  | fields              | reisdocumentnummer,houder  |
* __Dan__ heeft de response 0 reisdocumenten

### Scenario: de gezochte persoon bestaat niet

* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 987654321                  |
  | fields              | reisdocumentnummer,houder  |
* __Dan__ heeft de response 0 reisdocumenten

## Rule: bij zoeken van reisdocumenten met burgerservicenummer worden alleen reisdocumenten geleverd die volgens de registratie nog in het bezit zijn van de persoon


### Scenario: de gezochte persoon heeft het reisdocument ingeleverd

* __Gegeven__ de persoon met burgerservicenummer '000000152' heeft een 'reisdocument' met de volgende gegevens

  | naam                                                                    | waarde    |
  |-------------------------------------------------------------------------|-----------|
  | soort reisdocument (35.10)                                              | PN        |
  | nummer reisdocument (35.20)                                             | NE3663258 |
  | datum uitgifte Nederlands reisdocument (35.30)                          | 20131106  |
  | datum einde geldigheid reisdocument (35.50)                             | 20231106  |
  | datum inhouding dan wel vermissing Nederlands reisdocument (35.60)      | 20221229  |
  | aanduiding inhouding dan wel vermissing Nederlands reisdocument (35.70) | I         |
* __En__ de persoon heeft de volgende 'verblijfplaats' gegevens

  | gemeente van inschrijving (09.10) |
  |-----------------------------------|
  | 0800                              |
* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 987654321                  |
  | fields              | reisdocumentnummer         |
* __Dan__ heeft de response 0 reisdocumenten

### Scenario: de gezochte persoon heeft meerdere reisdocumenten ingeleverd en heeft één reisdocument nog in bezit

* __Gegeven__ de persoon met burgerservicenummer '000000152' heeft een 'reisdocument' met de volgende gegevens

  | naam                                                                    | waarde    |
  |-------------------------------------------------------------------------|-----------|
  | soort reisdocument (35.10)                                              | PN        |
  | nummer reisdocument (35.20)                                             | NE3663258 |
  | datum uitgifte Nederlands reisdocument (35.30)                          | 20131106  |
  | datum einde geldigheid reisdocument (35.50)                             | 20231106  |
  | datum inhouding dan wel vermissing Nederlands reisdocument (35.60)      | 20221229  |
  | aanduiding inhouding dan wel vermissing Nederlands reisdocument (35.70) | I         |
* __En__ de persoon heeft een 'reisdocument' met de volgende gegevens

  | naam                                           | waarde    |
  |------------------------------------------------|-----------|
  | soort reisdocument (35.10)                     | PN        |
  | nummer reisdocument (35.20)                    | NWE45TN71 |
  | datum uitgifte Nederlands reisdocument (35.30) | 20230317  |
  | datum einde geldigheid reisdocument (35.50)    | 20330317  |
* __En__ de persoon heeft een 'reisdocument' met de volgende gegevens

  | naam                                                                    | waarde    |
  |-------------------------------------------------------------------------|-----------|
  | soort reisdocument (35.10)                                              | PN        |
  | nummer reisdocument (35.20)                                             | PP82046A7 |
  | datum einde geldigheid reisdocument (35.50)                             | 20281103  |
  | datum inhouding dan wel vermissing Nederlands reisdocument (35.60)      | 20230205  |
  | aanduiding inhouding dan wel vermissing Nederlands reisdocument (35.70) | I         |
* __En__ de persoon heeft de volgende 'verblijfplaats' gegevens

  | gemeente van inschrijving (09.10) |
  |-----------------------------------|
  | 0800                              |
* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 000000152                  |
  | fields              | reisdocumentnummer         |
* __Dan__ heeft de response 1 reisdocumenten
* __En__ heeft de response een 'reisdocument' met de volgende gegevens

  | naam               | waarde    |
  |--------------------|-----------|
  | reisdocumentnummer | NWE45TN71 |

### Scenario: de gezochte persoon heeft reisdocumenten ingeleverd en vermist en heeft verschillende soorten reisdocumenten in bezit

* __Gegeven__ de persoon met burgerservicenummer '000000152' heeft een 'reisdocument' met de volgende gegevens

  | naam                                                                    | waarde    |
  |-------------------------------------------------------------------------|-----------|
  | soort reisdocument (35.10)                                              | PN        |
  | nummer reisdocument (35.20)                                             | NE3663258 |
  | datum uitgifte Nederlands reisdocument (35.30)                          | 20131106  |
  | datum einde geldigheid reisdocument (35.50)                             | 20231106  |
  | datum inhouding dan wel vermissing Nederlands reisdocument (35.60)      | 20221229  |
  | aanduiding inhouding dan wel vermissing Nederlands reisdocument (35.70) | I         |
* __En__ de persoon heeft een 'reisdocument' met de volgende gegevens

  | naam                                           | waarde    |
  |------------------------------------------------|-----------|
  | soort reisdocument (35.10)                     | PN        |
  | nummer reisdocument (35.20)                    | NWE45TN71 |
  | datum uitgifte Nederlands reisdocument (35.30) | 20230317  |
  | datum einde geldigheid reisdocument (35.50)    | 20330317  |
* __En__ de persoon heeft een 'reisdocument' met de volgende gegevens

  | naam                                                                    | waarde    |
  |-------------------------------------------------------------------------|-----------|
  | soort reisdocument (35.10)                                              | NI        |
  | nummer reisdocument (35.20)                                             | ID82046A7 |
  | datum einde geldigheid reisdocument (35.50)                             | 20281103  |
  | datum inhouding dan wel vermissing Nederlands reisdocument (35.60)      | 20230205  |
  | aanduiding inhouding dan wel vermissing Nederlands reisdocument (35.70) | V         |
* __En__ de persoon heeft een 'reisdocument' met de volgende gegevens

  | naam                                        | waarde    |
  |---------------------------------------------|-----------|
  | soort reisdocument (35.10)                  | NI        |
  | nummer reisdocument (35.20)                 | ID23NW456 |
  | datum einde geldigheid reisdocument (35.50) | 20330221  |
* __En__ de persoon heeft de volgende 'verblijfplaats' gegevens

  | gemeente van inschrijving (09.10) |
  |-----------------------------------|
  | 0800                              |
* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 000000152                  |
  | fields              | reisdocumentnummer         |
* __Dan__ heeft de response een 'reisdocument' met de volgende gegevens

  | naam               | waarde    |
  |--------------------|-----------|
  | reisdocumentnummer | NWE45TN71 |
* __En__ heeft de response een 'reisdocument' met de volgende gegevens

  | naam               | waarde    |
  |--------------------|-----------|
  | reisdocumentnummer | ID23NW456 |

## Rule: als een gevraagde veld in onderzoek is, dan wordt het bijbehorend inOnderzoek veld en datumIngangOnderzoek ook geleverd


### Scenario: 'soort reisdocument (35.10)' is in onderzoek en wordt gevraagd

* __Gegeven__ de persoon met burgerservicenummer '000000152' heeft een 'reisdocument' met de volgende gegevens

  | naam                                        | waarde    |
  |---------------------------------------------|-----------|
  | soort reisdocument (35.10)                  | PN        |
  | nummer reisdocument (35.20)                 | NE3663258 |
  | datum einde geldigheid reisdocument (35.50) | 20240506  |
  | aanduiding in onderzoek (83.10)             | 123510    |
  | datum ingang onderzoek (83.20)              | 20230201  |
* __En__ de persoon heeft de volgende 'verblijfplaats' gegevens

  | gemeente van inschrijving (09.10) |
  |-----------------------------------|
  | 0800                              |
* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 000000152                  |
  | fields              | reisdocumentnummer,soort   |
* __Dan__ heeft de response een 'reisdocument' met de volgende gegevens

  | naam                                         | waarde             |
  |----------------------------------------------|--------------------|
  | reisdocumentnummer                           | NE3663258          |
  | soort.code                                   | PN                 |
  | soort.omschrijving                           | Nationaal paspoort |
  | inOnderzoek.soort                            | true               |
  | inOnderzoek.datumIngangOnderzoek.type        | Datum              |
  | inOnderzoek.datumIngangOnderzoek.datum       | 2023-02-01         |
  | inOnderzoek.datumIngangOnderzoek.langFormaat | 1 februari 2023    |

### Scenario: 'soort reisdocument (35.10)' is in onderzoek en wordt niet gevraagd

* __Gegeven__ de persoon met burgerservicenummer '000000152' heeft een 'reisdocument' met de volgende gegevens

  | naam                                        | waarde    |
  |---------------------------------------------|-----------|
  | soort reisdocument (35.10)                  | PN        |
  | nummer reisdocument (35.20)                 | NE3663258 |
  | datum einde geldigheid reisdocument (35.50) | 20240506  |
  | aanduiding in onderzoek (83.10)             | 123510    |
  | datum ingang onderzoek (83.20)              | 20230201  |
* __En__ de persoon heeft de volgende 'verblijfplaats' gegevens

  | gemeente van inschrijving (09.10) |
  |-----------------------------------|
  | 0800                              |
* __Als__ reisdocumenten wordt gezocht met de volgende parameters

  | naam                | waarde                     |
  |---------------------|----------------------------|
  | type                | ZoekMetBurgerservicenummer |
  | burgerservicenummer | 000000152                  |
  | fields              | reisdocumentnummer         |
* __Dan__ heeft de response een 'reisdocument' met de volgende gegevens

  | naam               | waarde    |
  |--------------------|-----------|
  | reisdocumentnummer | NE3663258 |

