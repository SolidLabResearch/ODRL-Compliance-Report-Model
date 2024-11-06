# Compliance Report for an ODRL Policy with a Prohibition rule (access request)

## ODRL read request against ODRL read Prohibition (temporal constraints)

### Request
Requesting Party ALICE requests to READ resource X.

```ttl
@prefix ex: <http://example.org/> .
@prefix odrl: <http://www.w3.org/ns/odrl/2/>.

<urn:uuid:1bafee59-006c-46a3-810c-5d176b4be364> a odrl:Request ;
    odrl:uid <urn:uuid:1bafee59-006c-46a3-810c-5d176b4be364>;
    odrl:permission <urn:uuid:186be541-5857-4ce3-9f03-1a274f16bf59> .

<urn:uuid:186be541-5857-4ce3-9f03-1a274f16bf59> a odrl:Permission ;
    odrl:assignee ex:alice ;
    odrl:action odrl:read ;
    odrl:target ex:x .
```

### Policy
ZENO is data owner of resource X.
ALICE may not READ resource X.

```ttl
@prefix odrl: <http://www.w3.org/ns/odrl/2/> .
@prefix ex: <http://example.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

<urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> a odrl:Set ;
    odrl:uid <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    odrl:prohibition <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001>.

<urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> a odrl:Prohibition;
    odrl:action odrl:read;
    odrl:target ex:x;
    odrl:assignee ex:alice;
    odrl:assigner ex:zeno.
```

### State of the World
Current time is 11:20:10 on Monday 12th of February 2024.

```ttl
@prefix temp: <http://example.com/request/> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

temp:currentTime dct:issued "2024-02-12T11:20:10.999Z"^^xsd:dateTime .
```

### Compliance report

The Compliance Report for this scenario is the following: at 11:20:10 on Monday 12th of February 2024 (UTC-0), the prohibition is ACTIVE (all premises are satisfied), ATTEMPTED (a request has been made), and UNKNOWN (we have no idea of the performance state).

Therefore, the Deontic State is the following NONSET.

```ttl
@prefix ex: <http://example.org/> .
@prefix report: <http://example.com/report/temp/> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

ex:policyReport1 a report:PolicyReport;
    dct:created "2024-02-12T11:20:10.999Z"^^xsd:dateTime;
    report:policy <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc>;
    report:policyRequest <urn:uuid:1bafee59-006c-46a3-810c-5d176b4be364>;
    report:ruleReport ex:prohibitionReport1.

ex:prohibitionReport1 a report:ProhibitionReport ;
    report:rule <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> ; 
    report:ruleRequest <urn:uuid:186be541-5857-4ce3-9f03-1a274f16bf59> ; 
    report:activationState report:Active ;
    report:attemptState report:Attempted ;
    report:performanceState report:Unknown ;
    report:deonticState report:NonSet ;
    report:premiseReport ex:partyReport, ex:targetReport, ex:actionReport.

ex:partyReport a report:PartyReport;
    report:satisfactionState report:Satisfied .

ex:targetReport a report:TargetReport;
    report:satisfactionState report:Satisfied .

ex:actionReport a report:ActionReport;
    report:satisfactionState report:Satisfied . 
```

### Compliance report (we know the action is performed)

The Compliance Report for this scenario is the following: at 11:20:10 on Monday 12th of February 2024 (UTC-0), the prohibition is ACTIVE (all premises are satisfied), ATTEMPTED (a request has been made), and PERFORMED (Alice has performed the read action).

Therefore, the Deontic State is the following VIOLATED.

```ttl
@prefix ex: <http://example.org/> .
@prefix report: <http://example.com/report/temp/> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

ex:policyReport1 a report:PolicyReport;
    dct:created "2024-02-12T11:20:10.999Z"^^xsd:dateTime ; 
    report:policy <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    report:policyRequest <urn:uuid:1bafee59-006c-46a3-810c-5d176b4be364> ;
    report:ruleReport ex:prohibitionReport1 .

ex:prohibitionReport1 a report:ProhibitionReport ;
    report:rule <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> ; 
    report:ruleRequest <urn:uuid:186be541-5857-4ce3-9f03-1a274f16bf59> ; 
    report:activationState report:Active ;
    report:attemptState report:Attempted ;
    report:performanceState report:Performed ;
    report:deonticState report:Violated ;
    report:premiseReport ex:partyReport, ex:targetReport, ex:actionReport .

ex:partyReport a report:PartyReport;
    report:satisfactionState report:Satisfied .

ex:targetReport a report:TargetReport;
    report:satisfactionState report:Satisfied .

ex:actionReport a report:ActionReport;
    report:satisfactionState report:Satisfied . 
```

### Compliance report (we know the action will no longer be performed)

The Compliance Report for this scenario is the following: at 11:20:10 on Monday 12th of February 2024 (UTC-0), the prohibition is ACTIVE (all premises are satisfied), ATTEMPTED (a request has been made), and UNPERFORMED (Alice has not performed the action and can no longer do it).

Therefore, the Deontic State is the following FULFILLED.

```ttl
@prefix ex: <http://example.org/> .
@prefix report: <http://example.com/report/temp/> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

ex:policyReport1 a report:PolicyReport;
    dct:created "2024-02-12T11:20:10.999Z"^^xsd:dateTime ; 
    report:policy <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    report:policyRequest <urn:uuid:1bafee59-006c-46a3-810c-5d176b4be364> ;
    report:ruleReport ex:prohibitionReport1 .

ex:prohibitionReport1 a report:ProhibitionReport ;
    report:rule <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> ; 
    report:ruleRequest <urn:uuid:186be541-5857-4ce3-9f03-1a274f16bf59> ; 
    report:activationState report:Active ;
    report:attemptState report:Attempted ;
    report:performanceState report:Unperformed ;
    report:deonticState report:Fulfilled ;
    report:premiseReport ex:partyReport, ex:targetReport, ex:actionReport .

ex:partyReport a report:PartyReport;
    report:satisfactionState report:Satisfied .

ex:targetReport a report:TargetReport;
    report:satisfactionState report:Satisfied .

ex:actionReport a report:ActionReport;
    report:satisfactionState report:Satisfied . 
```