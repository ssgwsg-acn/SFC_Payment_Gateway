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



<b>STEP 1 – CREATING THE REQUEST PAYLOAD</b>

![](img/payment_processS1.png?raw=true "Payment Flow")

With the SFC Payment Gateway, users will be redirected to the payment page for an option to utilise their credit to offset against their course fees. e-Services must prepare a set of information, known as the payload, that is required by SSG to validate the user’s request to use their SFC.
The following sections will provide technical information regarding the requirements of the request payload. 

FIELD ATTRIBUTES
 
|Parameters|Mandatory|Type/Length|Description|
|--- |--- |--- |--- |
|NRIC|Y|String/9|To validate if the same NRIC is used for SingPass login|
|Mobile Number*|N|String/8|To pre-populate in contact details in SFC Payment Gateway only if the information is not available|
|Home Number*|N|String/8||
|Email Address*|N|String/241||
|TP UEN|Y|String/10|UEN of the Training Provider|
|Source ID|Y|String/6|To be provided to respective e-Services during onboarding. The source ID will be unique to each Training Provider/e-Service|
|Course ID|Y|String/50|External course reference number|
|Course Run ID|N|String/50|External course run reference number|
|Course Start Date|Y|String/10|Start date of the registered course. The format must be: yyyy-mm-dd|
|Course Fee Payable|Y|String/9|Net amount (including GST) of the course to validate against SFC Payment amount. The format must be to 2 decimal placing|
|Additional Info|N|String/512|For Training Provider's reference|

\* Note that for the initial claim request, contact information shared by the e-Service will be pre-populated if the user has not transacted with SSG/WSG before.

SAMPLE INITIAL CLAIM REQUEST PAYLOAD BEFORE ENCRYPTION<code><pre>{
	"nric":" S98xxx71J",
	"mobileno":"12345678",
	"homeno":"87654321",
	"email":"abc@yahoo.com",
	"uen":"19830XXX0C",
	"sourceId":"xxx0001",
	"courseID":"Fengshan 163",
	"courseRunId":"",
	"courseStartDate":"2018-02-10",
	"courseFee":"50.2",
	"addInfo":"This is additional information"
}</pre></code>
