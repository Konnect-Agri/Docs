---
sidebar_position: 4
sidebar_label: Consent Manager
---

# Consent Manager

Consent Manager is a part of Konnet Stack which handles the entire consent lifecycle. It is responsible for blocking data request transactions and provides authorization based on data owner's consent. This is direcly influenced from the <b>[Legal Framework for Mandatory Electronic Delivery of Services](https://www.meity.gov.in/sites/upload_files/dit/files/Consolidatep_PPT_02122010.pdf)</b> of Ministry of Communications and Information Technology, India. 

Talking in a broader sense of the vision of the inspiration, it's aiming for :
- Ensure more e-services are made available
- Ensure greater access to e-services
- e-Services being enabled through MMPs
- Access being ensured through e-infrastructure
- Need - Accelerate the e-enablement of services
- Phasing out of manual delivery of services

# Block Functions
- Authentication - Verifies the authenticity of a data consumer
- Consent artifact - A consent artifact is a machine-readable electronic document that specifies the parameters and scope of data that a user consents to in any data-sharing transaction. In this framework, consent must be digitally signed, either by the user or by the consent collector or both
- Authorization (GateKeeper) - Verifies if the Query requested has the required permisions from the data owner (farmer) (checks if query is a subset of Consent Artifact)
- Query Resolver - Verifies Queries and gets data from external sources/ or state databases
- Consent Manager - Creates and Manages the lifecycle of a Consent Artifact. From request, ,generation, and revoke/expiry
- UI for Consent Manager
- UI for User
---

# Building Blocks of Consent Manager

### Authenticator Layer 🔒
It is the very first layer/building block of consent manager. Every request routes through here and it handles all the authentication and authorization procedures.

### Decision Maker (Consent Manager)
The business logic layer which handles the creation, retrieval and modification of Consent Artifact (CA). This layer is responsbile for creating and associating Consent Artifacts with the respective users.

### Gatekeeper
It is just as the name sounds like, it acts like a guard which looks over what data is requested and what is delivered. The requested data must be a subset of the information allowed by the user that can be delivered.

### Resolver
The final layer which handles the actual logic of data retrieval and delivery. If all checks pass that is the user is properly authenticated,authorized and is requesting mindful data in compliance with the permitted information then the Resolver layer extracts the required information and sends it back.

To know more about it checkout the github repo <b>[here](https://github.com/Konnect-Agri/consent-manager)</b>


## Integration with SAFAL
![safalxconsentmanager (1) drawio](https://github.com/Konnect-Agri/consent-manager/assets/46066481/8635f5c4-f092-4f73-8d98-420a70f11f8d)
