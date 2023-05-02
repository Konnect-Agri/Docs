---
sidebar_position: 5
sidebar_label: Demo 2
---

# UFSI: search, select, init, confirm

### Objective - Creation of sample credit portal
- Enable farmers to digitally search, apply, and track loan products using a simple web portal
- Enable bank managers to track and take action on the loan requests/ applications submitted by the farmers

### Enabled use cases

1. Farmer - Logins into the credit portal 
2. Farmer - Searches for credit products with the following filters 
    1. District
    2. Block
    3. Bank

    (Search ⇒ A simple search request that returns a catalog as per Beckn core spec for the /on-search route)
    ![imageN](../../images/imageN.png)
3. Farmer - Selects one of the products shown on the table as per search criterion 

    (select ⇒ this action/route basically maps to creation of an order, hence an order will be created with the selected loan item)
4. Farmer - A draft credit order popups up, farmer is nudged to fill application form

    (init ⇒ this route actually deals with entering payment and shipping details, which will map to filling out the LoanApplicationForm in our use case)

    (future vision ⇒ once agridex (auth + consent manager) is working and we are able to link farmer data from KO, most info of the application form will be auto populated)

    [ Decisions on how init will render different application forms for different  products/ banks,
    - Init spec will include customisable application form query
        - will add a provider-specific (farmer) field “specific_applicant_details” which will be queried from a federated server and displayed to the user (bank) 
        - this will allow the bank to send the delta of their forms which does not conform with the “loan application doc” spec as JSON
        - Combination of the two will be the entire application form of the loan product ]

5. Farmer - Upon application submission, the order is routed to bank manager (loan officer) and the order is confirmed

    (confirm ⇒ in our use case this will be mapped to the bank manager (of loan officer) confirming our request has been successfully submitted for verification)

![image](../../images/image3.png)


