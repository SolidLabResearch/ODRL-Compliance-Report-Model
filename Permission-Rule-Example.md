# Compliance Report for an ODRL Policy with a Permission rule (access request)

## ODRL read request against ODRL read Permission (temporal constraints)

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
ALICE may READ resource X between 2024-01-01T00:00:00Z and 2024-12-31T00:00:00Z.

```ttl
@prefix odrl: <http://www.w3.org/ns/odrl/2/> .
@prefix ex: <http://example.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

<urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> a odrl:Set ;
  odrl:uid <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
  odrl:permission <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001>.

<urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> a odrl:Permission ;
  odrl:action odrl:read ;
  odrl:target ex:x ;
  odrl:assignee ex:alice ;
  odrl:assigner ex:zeno ;
  odrl:constraint <urn:uuid:c9359a6f-06bf-4a99-afb0-62996ca78100> .

<urn:uuid:c9359a6f-06bf-4a99-afb0-62996ca78100> a odrl:LogicalConstraint ;
    odrl:and <urn:uuid:c1a4d116-2777-4598-847d-8fbebf8eb535>, <urn:uuid:49e4be66-54ef-45e0-8fac-5d5eb58c23fd> .

<urn:uuid:c1a4d116-2777-4598-847d-8fbebf8eb535> a odrl:Constraint ;
    odrl:leftOperand odrl:dateTime ;
    odrl:operator odrl:gt ;
    odrl:rightOperand "2024-01-01T00:00:00Z"^^xsd:dateTime .

<urn:uuid:49e4be66-54ef-45e0-8fac-5d5eb58c23fd> a odrl:Constraint ;
    odrl:leftOperand odrl:dateTime ;
    odrl:operator odrl:lt ;
    odrl:rightOperand "2024-12-31T00:00:00Z"^^xsd:dateTime .

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

The Compliance Report for this scenario is the following: at 11:20:10 on Monday 12th of February 2024 (UTC-0), the permission is ACTIVE (all premises are satisfied), ATTEMPTED (a request has been made), and UNKNOWN (we have no idea of the performance state).

Therefore, the Deontic State is the following NONSET.

```ttl
@prefix ex: <http://example.org/> .
@prefix report: <https://w3id.org/force/compliance-report#> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

ex:policyReport1 a report:PolicyReport;
    dct:created "2024-02-12T11:20:10.999Z"^^xsd:dateTime ;
    report:policy <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    report:policyRequest <urn:uuid:1bafee59-006c-46a3-810c-5d176b4be364> ;
    report:ruleReport ex:permissionReport1 .

ex:permissionReport1 a report:PermissionReport ;
    report:rule <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> ; 
    report:ruleRequest <urn:uuid:186be541-5857-4ce3-9f03-1a274f16bf59> ; 
    report:activationState report:Active ;
    report:attemptState report:Attempted ;
    report:performanceState report:Unknown ;
    report:deonticState report:NonSet ;
    report:premiseReport ex:constraintReport1, ex:partyReport, ex:targetReport, ex:actionReport.

ex:constraintReport1 a report:ConstraintReport ;
    report:constraint <urn:uuid:c9359a6f-06bf-4a99-afb0-62996ca78100> ; 
    report:satisfactionState report:Satisfied ;
    report:constraintReport ex:constraintReport2, ex:constraintReport3 . 

ex:constraintReport2 a report:ConstraintReport ;
    report:constraint <urn:uuid:c1a4d116-2777-4598-847d-8fbebf8eb535> ; 
    report:satisfactionState report:Satisfied .

ex:constraintReport3 a report:ConstraintReport ;
    report:constraint <urn:uuid:49e4be66-54ef-45e0-8fac-5d5eb58c23fd> ; 
    report:satisfactionState report:Satisfied .

ex:partyReport a report:PartyReport;
    report:satisfactionState report:Satisfied .

ex:targetReport a report:TargetReport;
    report:satisfactionState report:Satisfied .

ex:actionReport a report:ActionReport;
    report:satisfactionState report:Satisfied . 
```

### Compliance report (we know the action is performed)

The Compliance Report for this scenario is the following: at 11:20:10 on Monday 12th of February 2024 (UTC-0), the permission is ACTIVE (all premises are satisfied), ATTEMPTED (a request has been made), and PERFORMED (Alice has performed the read action).

Therefore, the Deontic State is the following FULFILLED.

```ttl
@prefix ex: <http://example.org/> .
@prefix report: <https://w3id.org/force/compliance-report#> .
@prefix dct: <http://purl.org/dc/terms/>.
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>.

ex:policyReport1 a report:PolicyReport;
    dct:created "2024-02-12T11:20:10.999Z"^^xsd:dateTime ; 
    report:policy <urn:uuid:95efe0e8-4fb7-496d-8f3c-4d78c97829bc> ;
    report:policyRequest <urn:uuid:1bafee59-006c-46a3-810c-5d176b4be364> ;
    report:ruleReport ex:permissionReport1 .

ex:permissionReport1 a report:PermissionReport ;
    report:rule <urn:uuid:f5199b0a-d824-45a0-bc08-1caa8d19a001> ; 
    report:ruleRequest <urn:uuid:186be541-5857-4ce3-9f03-1a274f16bf59> ; 
    report:activationState report:Active ;
    report:attemptState report:Attempted ;
    report:performanceState report:Performed ;
    report:deonticState report:Fulfilled ;
    report:premiseReport ex:constraintReport1, ex:partyReport, ex:targetReport, ex:actionReport.

ex:constraintReport1 a report:ConstraintReport ;
    report:constraint <urn:uuid:c9359a6f-06bf-4a99-afb0-62996ca78100> ; 
    report:satisfactionState report:Satisfied ;
    report:constraintReport ex:constraintReport2, ex:constraintReport3 . 

ex:constraintReport2 a report:ConstraintReport ;
    report:constraint <urn:uuid:c1a4d116-2777-4598-847d-8fbebf8eb535> ; 
    report:satisfactionState report:Satisfied .

ex:constraintReport3 a report:ConstraintReport ;
    report:constraint <urn:uuid:49e4be66-54ef-45e0-8fac-5d5eb58c23fd> ; 
    report:satisfactionState report:Satisfied .

ex:partyReport a report:PartyReport;
    report:satisfactionState report:Satisfied .

ex:targetReport a report:TargetReport;
    report:satisfactionState report:Satisfied .

ex:actionReport a report:ActionReport;
    report:satisfactionState report:Satisfied . 
```