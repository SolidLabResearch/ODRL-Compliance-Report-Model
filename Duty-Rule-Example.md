# Compliance Report for an ODRL Policy with a Duty rule

## ODRL Duty: Alice must delete a resource

### Policy
ALICE must DELETE resource X.

```ttl
@prefix odrl: <http://www.w3.org/ns/odrl/2/> .
@prefix ex: <http://example.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

<urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> a odrl:Set ;
    odrl:uid <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    odrl:duty <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001>.

<urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> a odrl:Duty;
    odrl:action odrl:delete;
    odrl:target ex:x;
    odrl:assignee ex:alice.
```

### State of the World
Current time is 11:20:10 on Monday 12th of February 2024.

```ttl
@prefix temp: <http://example.com/request/> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

temp:currentTime dct:issued "2024-02-12T11:20:10.999Z"^^xsd:dateTime .
```

### Compliance Report

The Compliance Report for this scenario is the following: at 11:20:10 on Monday 12th of February 2024 (UTC-0), the prohibition is ACTIVE (all premises are satisfied) and UNKNOWN (we have no idea of the performance state).

Therefore, the Deontic State is the following NONSET.

```ttl
@prefix ex: <http://example.org/> .
@prefix report: <https://w3id.org/force/compliance-report#> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

ex:policyReport1 a report:PolicyReport;
    dct:created "2024-02-12T11:20:10.999Z"^^xsd:dateTime ; 
    report:policy <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    report:ruleReport ex:dutyReport1 .

ex:dutyReport1 a report:DutyReport ;
    report:rule <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> ; 
    report:activationState report:Active ;
    report:performanceState report:Unknown ;
    report:deonticState report:NonSet .
```

### Compliance report (we know the action is performed)

The Compliance Report for this scenario is the following: at 11:20:10 on Monday 12th of February 2024 (UTC-0), the prohibition is ACTIVE (all premises are satisfied) and PERFORMED (Alice has performed the delete action).

Therefore, the Deontic State is the following FULFILLED.

```ttl
@prefix ex: <http://example.org/> .
@prefix report: <https://w3id.org/force/compliance-report#> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

ex:policyReport1 a report:PolicyReport;
    dct:created "2024-02-12T11:20:10.999Z"^^xsd:dateTime ; 
    report:policy <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    report:ruleReport ex:dutyReport1 .

ex:dutyReport1 a report:DutyReport ;
    report:rule <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> ; 
    report:activationState report:Active ;
    report:performanceState report:Performed ;
    report:deonticState report:Fulfilled .
```

### Compliance report (we know the action will no longer be performed)

The Compliance Report for this scenario is the following: at 11:20:10 on Monday 12th of February 2024 (UTC-0), the prohibition is ACTIVE (all premises are satisfied) and UNPERFORMED (Alice has not performed the action and can no longer do it).

Therefore, the Deontic State is the following VIOLATED.

```ttl
@prefix ex: <http://example.org/> .
@prefix report: <https://w3id.org/force/compliance-report#> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

ex:policyReport1 a report:PolicyReport;
    dct:created "2024-02-12T11:20:10.999Z"^^xsd:dateTime ; 
    report:policy <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    report:ruleReport ex:dutyReport1 .

ex:dutyReport1 a report:DutyReport ;
    report:rule <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> ; 
    report:activationState report:Active ;
    report:performanceState report:Unperformed ;
    report:deonticState report:Violated .
```