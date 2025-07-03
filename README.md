# ODRL Compliance Report Model


[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.14193486.svg)](https://doi.org/10.5281/zenodo.14193486)


A Compliance Report is our proposed output for an [Open Digitial Rights Language (ODRL)](https://www.w3.org/TR/odrl-model/) Policy.

The informal definition is the following: *"A vocabulary that is used to elaborate the result of an evaluation of an ODRL Policy, (optionally) ODRL Request and the state of the world. <br>
It elaborates not only **whether** a rule from a policy is active, but also **why**."*

It has been modelled by taking in the [specification of the ODRL Formal Semantics](https://w3c.github.io/odrl/formal-semantics/) and iterated upon through discussions between Beatriz and Wout.

The ODRL Compliance Report Model can be found at the root of this repository: [`ComplianceReportModel.ttl`](./ComplianceReportModel.ttl)

Below is a visualisation of this report.

![visualization of the compliance report model](<./img/Compliance Report Model.svg>)

## Examples

For each type of [ODRL Rule](https://www.w3.org/TR/odrl-model/#rule), an example is worked out:

- [Permission Rule Example](./Permission-Rule-Example.md)
- [Prohibition Rule Example](./Prohibition-Rule-Example.md)
- [Duty Rule Example](./Duty-Rule-Example.md)

Note: since no formalisation exist on the inputs apart from the ODRL Policy itself for the generation of output (the compliance report), a decision was made such that an evaluation is a safe, deterministic operation and thus strictly dependent on its inputs:
- A time triple is present as state of the world (e.g. `temp:currentTime dct:issued "2024-01-01T00:00:00"^^xsd:dateTime .`)
- For the access control scenario, an ODRL Request Policy is used with a Permission rule. This can then be read as follows: *"Is the **assignee** allowed to perform the particular **action** on a given **target** resource?"*.

## Elaboration of satisfaction, activation, attempted, performance, deontic states

### Satisfaction state

Relates to all premises of a rule.
Such premises include ODRL constraint (also logical constraint), target premise (does the requested resource fulfill the conditions of the target of the policy rule), action premise (does the requested action fulfill the conditions of the action of the policy rule), and party premise (does the requesting party match the conditions of the assignee of the policy rule).

A premise can thus be **satisfied** or **not satisfied**. <br>
If not information is present to fulfill the premise, then, at that time, the premise is **not satisfied**.

### Activation state

If and only if all premises of a rule are satisfied, then the rule is **active**.

Otherwise, the rule is **inactive**.

### Attempted state

If a requesting party made a request to perform a certain action a certain target resource, then the rule is **attempted**.

If there was no such access request, then the rule is **not attempted**.

### Performance state

This relates to the action of the rule.

If the action of the rule is executed, then the state is **performed**. <br>
If the action of the rule is not executed and it is known that it can no longer be executed, then the state is **unperformed**. <br>
If the action of the rule is not executed, but it could still be executed, then the state is **unknown**. <br>
*The unknown state could thus also be used in scenarios where no information is present about whether the action was or was not executed*


### Deontic state

This relates to whether it was okay for a given action to be executed, whether the action should have been executed, or whether it should not have been executed.

- fulfilled means that when action is executed, that was something that is allowed to happen and when it is not executed, it indeed should not have been.
- violated means that when an action is executed, it should not have been and when it is not executed, it should have been.
- not-set means that there is not enough information to make the decision. This is the case when for example when a duty for a permission is not fulfilled, but it is still possible to fulfill it (e.g. the deadline was only tomorrow) .

| activation state | performance state | deontic concept | deontic state |
| ---------------- | ----------------- | --------------- | ------------- |
| Active           | Performed         | Permission      | fulfilled     |
| Active           | Performed         | Prohibition     | violated      |
| Active           | Performed         | Duty            | fulfilled     |
| Active           | Unperformed       | Permission      | not-set       |
| Active           | Unperformed       | Prohibition     | fulfilled     |
| Active           | Unperformed       | Duty            | violated      |
| Active           | Unknown           | Permission      | not-set       |
| Active           | Unknown           | Prohibition     | not-set       |
| Active           | Unknown           | Duty            | not-set       |
| Inactive         | Performed         | Permission      | violated      |
| Inactive         | Performed         | Prohibition     | not-set       |
| Inactive         | Performed         | Duty            | not-set       |
| Inactive         | Unperformed       | Permission      | fulfilled     |
| Inactive         | Unperformed       | Prohibition     | not-set       |
| Inactive         | Unperformed       | Duty            | not-set       |
| Inactive         | Unknown           | Permission      | not-set       |
| Inactive         | Unknown           | Prohibition     | not-set       |
| Inactive         | Unknown           | Duty            | not-set       |

## Feedback and questions

Do not hesitate to [report a bug](https://github.com/woutslabbinck/UCR-test-suite/issues).

Further questions can also be asked to [Wout Slabbinck](mailto:wout.slabbinck@ugent.be) (developer and maintainer of this repository).
