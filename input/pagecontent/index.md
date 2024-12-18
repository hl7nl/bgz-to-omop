### Pipeline

![pipeline](pipeline.png)
<div style="clear:both;">
</div>

### Minutes

* relatie met Vulcan opbouwen [FHIR to OMOP](https://build.fhir.org/ig/HL7/fhir-omop-ig/artifacts.html), gaat waarschijnlijk MAY2025 in [ballot](https://www.hl7.org/BallotDesktop)
    * relevante OMOP logical models toevoegen (o.a. condition_occurrence) uit FHIR to OMOP
* pipeline beschrijven obv HRI hackathon (zie plaatje boven)
    * StructureMap/FML versie van ViewDefinitions maken
        * Condition FML @Michael
        * Drug Exposure FML @Sebastiaan
    * eerst FML, dan ViewDefinition zodat je eea kan toepassen in b.v. [Google Open Health Stack](https://developers.google.com/open-health-stack/fhir-analytics/view-layer)
    * Pseudonomize stap en [Microsoft Tools-for-Health-Data-Anonymization](https://github.com/microsoft/Tools-for-Health-Data-Anonymization) stappen uitleggen
* Condition.verificationStatus = confirmed; en hoe doe je dit met de andere resources?
* metadata toevoegen; periode van de selectie; 1 jaar aan data; query datum; bepaald specialisme; welke organisatie
    * Bulk FHIR obv een cohort/study/registry/group
    * Kan ViewDefinition op ndjson werken ipv Bundle?
* FHIR id's zijn geen integers, moeten via lookup opgezocht worden, dus person_id via lookup naar person.person_source_value == FHIR Patient.id 
    * dit geld ook voor codes (naar OMOP vocabulary tables o.a. concept)
    * hoe om te gaan met meerdere codings
* resource type correctie; als je een Condition via een Observation stuurt (e.g. via een SDE), kan je in de OMOP vocabulary vinden dat hier een conversie nodig is via de OMOP Domain ID (= tabel) https://ohdsi.github.io/CommonDataModel/cdm54.html#concept
* OMOP source-value/concept-id = meest precieze code /die gekozen is bij registratie/ (DHD DT) die je hebt geregistreerd
    * (FHIR)Condition.code.text is de source-value display of gewijzigd door de registrator
    * concept_id = gestandaardiseerde code SNOMED CT, LOINC
    * Context is MSZ, dan is de DHD de source
    * Context is HA, dan is de ICPC/NHG de source
    * ...

### ViewDefinitions

* [ViewDefinition-OMOP-condition_occurrence](ViewDefinition-OMOP-condition_occurrence.json)
* [ViewDefinition-OMOP-visit_occurence](ViewDefinition-OMOP-visit_occurence.json)

### Dependencies

* FHIR to OMOP gaat januari 2025 in ballot. Als die gepublished is kunnen we daarop dependen, nu even gecopyeerd uit de [CI-build](https://build.fhir.org/ig/HL7/fhir-omop-ig/).
```json
    "dependsOn": [
    {
      "uri": "http://hl7.org/fhir/uv/omop/ImplementationGuide/hl7.fhir.uv.omop",
      "packageId": "hl7.fhir.uv.omop",
      "version": "0.1.0"
    } ]
```

{% include dependency-table.xhtml %}
