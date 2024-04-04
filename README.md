# BGZ-to-OMOP

* Poster "Leveraging FHIR for a generic EHR to OMOP-ETL: can we make an ETL process reusable?"
* BgZ als FHIR Bundle omzetten naar OMOP voor hergebruik in onderzoek.
* Waar lopen we tegenaan?
* Later ook proberen IPS, e.g. op basis van de $ips operation van Epic
* Definieer StructMaps van OMOP logical models (https://build.fhir.org/ig/HL7/fhir-omop-ig/) naar zibs2017/STU3 FHIR
* Eventueel ook kijken naar SQL-on-FHIR (https://build.fhir.org/ig/FHIR/sql-on-fhir-v2/) view definitions 

# Docker to run IG Publisher
```
> docker run --name=bgz-to-omop -it -v "$(pwd)":/app node:lts-buster /bin/bash
```
.. install GoFSH and sushi, see https://fshschool.org/docs/gofsh/installation/

.. install java, jekyll, graphviz (needed for plantuml) in Docker (required for IG tooling)

```
@> apt update
@> apt install jekyll graphviz
@> dpkg -i jdk-21_linux-x64_bin.deb
@> npm install -g fsh-sushi
```
N.B. npm gofsh doesnot work in GitHub workflows, but npm fsh-sushi does?

# Validate resources
```
> curl -L https://github.com/hapifhir/org.hl7.fhir.core/releases/latest/download/validator_cli.jar -o validator_cli.jar
> java -jar validator_cli.jar -version 3.0.2 input/resources
```

# Build IG
```
> curl -L https://github.com/HL7/fhir-ig-publisher/releases/latest/download/publisher.jar -o publisher.jar
> java -jar publisher.jar -ig ig.ini
```

# Bevindingen

* SUSHI ondersteund STU3 niet
    * WORKAROUND: run sushi to generate R4 en pas de R4 logical models aan naar STU3 en gebruik die als input/resources
        * fhirVersion 3.0.2
        * element.type.targetProfile is geen array in STU3
* Logical Models geven error bij valideren, maar IG wordt wel gemaakt
* FML niet ondersteund in STU3
    * WORKAROUND: definieer StructMaps