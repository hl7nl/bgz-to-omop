### Pipeline

![pipeline](pipeline.png)
<div style="clear:both;">
</div>

### TODO

* relatie met Vulcan FHIR to OMOP
* pipeline beschrijven obv HRI hackathon (zie boven)
* Condition.verificationStatus = confirmed; en hoe doe je dit met de andere resources?
* metadata toevoegen; periode van de selectie; 1 jaar aan data; query datum; bepaald specialisme; welke organisatie
    * Bulk FHIR obv een cohort/study/registry/group
    * Kan ViewDefinition op ndjson werken ipv Bundle?
* Pseudostap en tool uitleggen
* FHIR id's zijn geen integers, moeten via lookup opgezocht worden, dus person_id via lookup naar person.person_source_value == FHIR Patient.id 
    * dit geld ook voor codes (naar OMOP vocabulary tables o.a. concept)
    * hoe om te gaan met meerdere codings
* relevante OMOP logical models toevoegen (o.a. condition_occurrence)
* FML versie van ViewDefinitions
* resource type correctie; als je een Condition via een Observation stuurt (e.g. via een SDE), kan je in de OMOP vocabulary vinden dat hier een conversie nodig is via de OMOP Domain ID (= tabel) https://ohdsi.github.io/CommonDataModel/cdm54.html#concept

### OMOP Logical Models

Copied OMOP Logical Models from the Vulcan [FHIR to OMOP IG](https://github.com/HL7/fhir-omop-ig/tree/main/input/fsh).

### ViewDefinitions

* [ViewDefinition-OMOP-condition_occurrence](ViewDefinition-OMOP-condition_occurrence.json)
* [ViewDefinition-OMOP-visit_occurence](ViewDefinition-OMOP-visit_occurence.json)

### Dependencies

{% include dependency-table.xhtml %}
