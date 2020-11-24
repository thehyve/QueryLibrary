<!---
Group:drug exposure
Name:DEX22 How many poeple take a drug in a given class?
Author:Patrick Ryan
CDM Version: 5.3
-->

# DEX22: How many poeple take a drug in a given class?

## Description

## Query
The following is a sample run of the query. The input parameters are highlighted in  blue. S

```sql
SELECT COUNT(DISTINCT d.person_id) AS person_count
  FROM @vocab.concept_ancestor ca
  JOIN @vocab.drug_exposure d
    ON d.drug_concept_id = ca.descendant_concept_id
 WHERE ca.ancestor_concept_id = 4324992
 GROUP BY ca.ancestor_concept_id;
```

## Input

|  Parameter |  Example |  Mandatory |  Notes |
| --- | --- | --- | --- |
| ancestor_concept_id | 4324992 |  Yes | Antithrombins |

## Output

|  Field |  Description |
| --- | --- |
| person_count | A foreign key that refers to a standard concept identifier in the vocabulary for the drug concept. |

## Example output record

|  Field |  Description |
| --- | --- |
| person_count |   |

## Documentation
https://github.com/OHDSI/CommonDataModel/wiki/
