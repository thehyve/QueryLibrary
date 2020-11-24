<!---
Group:thehyve
Name:Hyve01 Clinical events
Author:Maxim Moinat
CDM Version: 5.3
-->

# Hyve01: Clinical events

## Description
Get all the clinical events (visits, conditions, drugs, procudures and observations) for a random person.

## Query
```sql
with clinical_events as (
    SELECT
        'Visit' AS domain_name, 
        person_id, 
        visit_start_date AS start_date, 
        visit_end_date AS end_date,
        visit_concept_id AS concept_id, 
        visit_type_concept_id as type_concept_id, 
        visit_source_value AS source_value,
        visit_occurrence_id, 1 as sort_order
    FROM @cdm.visit_occurrence

    UNION
    SELECT
        'Condition' AS domain_name, 
        person_id, 
        condition_start_date AS start_date, 
        condition_end_date AS end_date,
        condition_concept_id AS concept_id, 
        condition_type_concept_id as type_concept_id, 
        condition_source_value AS source_value,
        visit_occurrence_id, 2 as sort_order
    FROM @cdm.condition_occurrence

    UNION

    SELECT
        'Drug' AS domain_name, person_id, 
        drug_exposure_start_date AS start_date, 
        drug_exposure_end_date AS end_date,
        drug_concept_id AS concept_id, 
        drug_type_concept_id as type_concept_id, 
        drug_source_value AS source_value,
        visit_occurrence_id, 3 as sort_order
    FROM @cdm.drug_exposure

    UNION

    SELECT
        'Procedure' AS domain_name, 
        person_id, 
        procedure_date AS start_date, 
        NULL AS end_date,
        procedure_concept_id AS concept_id, 
        procedure_type_concept_id as type_concept_id, 
        procedure_source_value AS source_value,
        visit_occurrence_id, 4 as sort_order
    FROM @cdm.procedure_occurrence

    UNION

    SELECT
        'Observation' AS domain_name, 
        person_id, 
        observation_date AS start_date, 
        NULL AS end_date,
        observation_concept_id AS concept_id, 
        observation_type_concept_id as type_concept_id, 
        observation_source_value AS source_value,
        visit_occurrence_id, 5 as sort_order
    FROM @cdm.observation
)
select 
	person_id, 
	domain_name, 
	start_date, 
    end_date, 
	event.concept_name as event_name,
    source_value,
	type.concept_name as type_name,
	visit_occurrence_id	
from clinical_events
   join @vocab.concept as event using(concept_id)
   join @vocab.concept as type on type.concept_id = type_concept_id
where person_id IN (select person_id from clinical_events order by random() limit 1)
order by person_id, start_date, sort_order, type.concept_name
```

## Input

No input

## Output

| Field            | Description                                                   |
| ---------------- | ------------------------------------------------------------- |
| person_id         | |
| domain_name       | |
| start_date        | |
| end_date          | |
| event_name        | |
| source_value      | |
| type_name         | |
| visit_occurence_id | |

## Example output record

| Field            | Value                                                   |
| ---------------- | ------------------------------------------------------------- |
| person_id         | |
| domain_name       | |
| start_date        | |
| end_date          | |
| event_name        | |
| source_value      | |
| type_name         | |
| visit_occurence_id | |


;