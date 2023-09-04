# Reviewing BPMN as a Modeling Notation for CACAO Security Playbooks

**Abstract:** As cyber systems become increasingly complex and cybersecurity threats become more prominent, defenders must prepare, coordinate, automate, document, and share their response methodologies to the extent possible. The CACAO standard was developed to satisfy the above requirements providing a common machine-readable framework and schema to document cybersecurity operations processes, including defensive tradecraft and tactics, techniques, and procedures. Although this approach is compelling, a remaining limitation is that CACAO provides no native modeling notation for graphically representing playbooks, which is crucial for simplifying their creation, modification, and understanding. In contrast, the industry is familiar with BPMN, a standards-based modeling notation for business processes that has also found its place in representing cybersecurity processes. This research examines BPMN and CACAO and explores the feasibility of using the BPMN modeling notation to graphically represent CACAO security playbooks. The results indicate that mapping CACAO and BPMN is attainable at an abstract level; however, conversion from one encoding to another introduces a degree of complexity due to the multiple ways CACAO constructs can be represented in BPMN and the extensions required in BPMN to fully support CACAO.

**Read the full paper:**\
M. Zych, V. Mavroeidis, K. Fysarakis and M. Athanatos, "Reviewing BPMN as a Modeling Notation for CACAO Security Playbooks," 2023 IEEE International Conference on Cyber Security and Resilience (CSR), Venice, Italy, 2023, pp. 490-495, doi: 10.1109/CSR57506.2023.10224922.  
Accessible preprint (arXiv): [Reviewing BPMN as a Modeling Notation for CACAO Security Playbooks](https://arxiv.org/pdf/2305.18928.pdf)

## CACAO-BPMN Mapping Table

The mapping between CACAO 2.0 and BPMN 2.0 specifications from [1].
![CACAO-BPMN Mapping](/CACAO-BPMN_Mapping.jpg)\
***Figure 1:** Mapping table retrieved from [1].*

## CACAO-BPMN Mapping: Use Case

In November 2021 the Cybersecurity Information Security Agency (CISA) has published the Cybersecurity Incident & Vulnerability Response Playbook to operational the procedures for planning and conducting cybersecurity incident and vulnerability response activities in Federal Civilian Executive Branch (FCEB) information system [2].

## Vulnerability Response Process

This template playbook describes the vulnerability response process in terms of standard vulnerability management program phases from [2].

![CISA template playbook!](CISA%20template%20playbook.png "CISA template playbook")\
***Figure 2:** Vulnerability Response Process. Retrieved from [2] page 22.*

## CACAO Playbook - JSON

CACAO playbook in JSON representing the vulnerability response process from Figure 2.

```json
{
  "type": "playbook",
  "spec_version": "cacao-2.0",
  "id": "playbook--59cef9c2-1944-4265-9f0f-0682693596cf",
  "name": "Vulnerability Response Process",
  "description": "Standard vulnerability management programs include phases for identifying, analyzing, remediating, and reporting vulnerabilities. This playbook describes the vulnerability response process in terms of standard vulnerability management program phases. ",
  "created_by": "identity--f0facbf9-aa22-4daf-b781-1f4d5cb96d87",
  "created": "2023-09-04T14:35:06.149Z",
  "modified": "2023-09-04T14:35:08.500Z",
  "revoked": false,
  "derived_from": [
    "playbook--187ed08f-64e5-4cef-badf-13058bf55214"
  ],
  "workflow_start": "start--976ad7a1-53c8-4e19-9635-96011d6bf4f7",
  "workflow": {
    "start--976ad7a1-53c8-4e19-9635-96011d6bf4f7": {
      "on_completion": "action--ba1b53c9-0a41-449e-b642-d7a44373bcda",
      "type": "start"
    },
    "action--ba1b53c9-0a41-449e-b642-d7a44373bcda": {
      "name": "Identification of Actively Exploited Vulnerability in the Wild.",
      "on_completion": "if-condition--5060d144-9535-4b75-bea5-0b477f7249bf",
      "type": "action"
    },
    "if-condition--5060d144-9535-4b75-bea5-0b477f7249bf": {
      "name": "Vulnerability Present?",
      "on_completion": "end--19eb2990-fc40-4cbc-84f1-22c8ca357526",
      "type": "if-condition",
      "on_true": "parallel--6020e6a6-7f3e-42e0-9c6c-df080fd93508",
      "on_false": "action--4502d396-fdb8-45be-a937-6c02ab97a521"
    },
    "action--4502d396-fdb8-45be-a937-6c02ab97a521": {
      "name": "As Directed, Report Status to CISA.",
      "on_completion": "end--2aa9ce57-3e60-4a72-a006-1e23a0f6e5bb",
      "type": "action"
    },
    "end--2aa9ce57-3e60-4a72-a006-1e23a0f6e5bb": {
      "type": "end"
    },
    "parallel--6020e6a6-7f3e-42e0-9c6c-df080fd93508": {
      "on_completion": "end--f710a35e-ad4b-4b05-b9d9-8cb5b852bdb6",
      "type": "parallel",
      "next_steps": [
        "if-condition--71df8f84-78d8-43d4-97b7-2476eb8eeae9",
        "if-condition--24c4a75b-fc4b-4b1f-b85b-cf66719bf6e0"
      ]
    },
    "if-condition--71df8f84-78d8-43d4-97b7-2476eb8eeae9": {
      "name": "Can you patch?",
      "on_completion": "end--4e825c5c-7847-4889-99cc-3b367a5e0e5b",
      "type": "if-condition",
      "on_true": "action--870a3b59-d945-423f-b46f-ff102a58e318",
      "on_false": "action--8263a75a-4e75-4657-be46-253a4a3835fb"
    },
    "if-condition--24c4a75b-fc4b-4b1f-b85b-cf66719bf6e0": {
      "name": "Signs of Exploitation?",
      "on_completion": "end--5b982431-6ee0-4273-8cd4-b7a26f13184d",
      "type": "if-condition",
      "on_true": "action--520c3ccd-b7b6-4a8f-9f9f-f5a0dd9a078f"
    },
    "action--520c3ccd-b7b6-4a8f-9f9f-f5a0dd9a078f": {
      "name": "Report to IR Team IR process starts",
      "on_completion": "action--4502d396-fdb8-45be-a937-6c02ab97a521",
      "type": "action"
    },
    "action--870a3b59-d945-423f-b46f-ff102a58e318": {
      "name": "Patch",
      "on_completion": "action--4502d396-fdb8-45be-a937-6c02ab97a521",
      "type": "action"
    },
    "action--8263a75a-4e75-4657-be46-253a4a3835fb": {
      "name": "Mitigate",
      "on_completion": "action--4502d396-fdb8-45be-a937-6c02ab97a521",
      "type": "action"
    },
    "end--f710a35e-ad4b-4b05-b9d9-8cb5b852bdb6": {
      "type": "end"
    },
    "end--19eb2990-fc40-4cbc-84f1-22c8ca357526": {
      "type": "end"
    },
    "end--4e825c5c-7847-4889-99cc-3b367a5e0e5b": {
      "type": "end"
    },
    "end--5b982431-6ee0-4273-8cd4-b7a26f13184d": {
      "type": "end"
    }
  }
}
```

## Translating to BPMN

Utilizing CACAO-BPMN mapping table to visualize the CACAO playbook as BPMN process.
![Vulnerability response BPMN modeling notation](/vulnerability-response-bpmn.png)\
***Figure 3:** CACAO playbook translated to BPMN process.*

## Resources

[1] M. Zych, V. Mavroeidis, K. Fysarakis and M. Athanatos, "Reviewing BPMN as a Modeling Notation for CACAO Security Playbooks," 2023 IEEE International Conference on Cyber Security and Resilience (CSR), Venice, Italy, 2023, pp. 490-495, doi: 10.1109/CSR57506.2023.10224922.  
Accessible preprint (arXiv): [Reviewing BPMN as a Modeling Notation for CACAO Security Playbooks](https://arxiv.org/pdf/2305.18928.pdf)

[2] [Cybersecurity Incident & Vulnerability Response Playbooks](https://www.cisa.gov/sites/default/files/publications/Federal_Government_Cybersecurity_Incident_and_Vulnerability_Response_Playbooks_508C.pdf) (cisa.gov)
