# SkillsFuture Credit (SFC) Payment Gateway Services
SFC Payment Gateway Request


Guidelines and interface specifications to the SkillsFuture Credit (SFC) Payment Gateway. This document is intended for the following users from Training Providers (TPs) for their e-Services:

•	Functional Users who require instructions on preparing their systems for technical integration with the SFC Payment Gateway <br>
•	Business Users who require an overview of the technical processes


The SFC Payment Gateway provides users with the opportunity to use their SFC at the point of registration for the course. During the registration process, users will be redirected to the SFC Payment Gateway to indicate the amount of credit they would like to use to offset their payment. 
The figure below shows a summary of the process and the steps to be taken by e-Services

![](img/payment_process.png?raw=true "Payment Flow")


 	Step 1 – Creating the Request Payload
The e-Service will create a request payload, which comprises of information (e.g. Course Start Date and Course Fee) that is necessary for SSG to allow the user to use their SkillsFuture Credit.

 	Step 2 – Encrypting the Request Payload
The e-Service will then encrypt the request payload using Trust Certificates provided by SSG. This is to ensure that the data transfer between the e-Service and SSG is secure and all information is kept confidential. 

 	Step 3 – Sending the Encrypted Request Payload
The e-Service will then send the encrypted request payload to SSG’s SFC Payment Gateway by calling the API via the URLs provided. The user will then be redirected to the SFC Payment Gateway page to complete their SFC claim application.

 	Step 4 – Decrypting the Encrypted Response Payload
After the user has completed the SFC claim process, the user will be redirected back to the e-Service, together with an encrypted response payload. The e-Service will decrypt the response payload using the Trust Certificates provided by SSG.

 	Step 5 – Reading the Response Payload
The e-Service will read the response payload after decryption. The response payload comprises of information that are necessary for the e-Service to continue the registration process with the user and continue the payment process for any outstanding amount.

 	Step 6 – Consuming APIs for further processing
The e-Service will upload supporting documents to SSG to support the SFC claim by the user. The e-Service may also choose to view or cancel the user’s claim. All these functionalities will be made available by consuming APIs made available to e-Services.

Do note that this process is applicable for every user transaction and will be performed automatically by the system. The different steps will be further detailed and explained in the subsequent sections.
Additionally, the successful submission of claims by users is dependent on the completion of payment and the upload of supporting documents. All claim submissions are subjected to approval by SSG.



STEP 1 – CREATING THE REQUEST PAYLOAD
