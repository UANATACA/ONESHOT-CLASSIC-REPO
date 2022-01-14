# What it is

<div style="text-align: justify">
The solution for electronic signature with a One Time certificate issue. One-Shot API is the solution for Uanataca One-Shot Signature service, a complete option for the electronic signature of documents within your application or web.
<br></br>
It is designed so that no sensitive data has to be sent away from your premises, as only hashes of the documents to be signed need to be transmitted to the signature service. Documents are signed through the creation of single-use digital certificates, which are created at the moment for immediately be used to electronically sign all documents included in a given transaction.
<br></br> 
Electronic signatures include a time stamp, providing to the document signature with a reliable date and time.
<br></br>
Through this system we offer our One-shot Signature service, an autonomous solution adapting to multiple use cases.
</div>

# How it works

<div style="text-align: justify">
The API is given with One-Shot Optimizer that is a server system exposing http RESTful API by means of which, business applications are enabled to require the electronic signature.
<br></br>
One-Shot Optimizer performs the most computationally expensive workload of the signature process, thus reducing the data traffic on the local network and make the most of the cryptographic hardware acceleration. The documents to be signed are processed in the customer business layer and are not send to Uanataca Services, instead is sent a hash of the document created using a hash algorithm.
<br></br>
Uanataca is a Qualified Trusted Service Provider that issue digital certificates by a trusted Certification Authority (CA). The role of Registration Authority Officials (RAO) is needed to add new user requests to the infrastructure and so request the creation of new digital certificates for its users. Each of these certificates can then be used to electronically sign documents.
<br></br>
One-Shot Signature certificates are generated on the spot every time a new set of documents requires a signature. Through the One-Shot Signature service, you will play the role of a RAO, providing identifying data for each user and requesting the generation of signature certificates. Once user registration data has been provided and the certificate is ready to be generated, the end user will activate the generation of the digital certificate and complete the signature procedure.
<br></br>
The electronic signatures are performed in Uanataca Trusted Service Center side, where signature keys are generated and stored in a Qualified Electronic Signature Creation Device (QSCD) system.
</div>
<br></br>

![img](https://github.com/UANATACA/ONESHOT-REPO/raw/main/img/oneshot-hiw.png)


# Flow chart

<div style="text-align: justify">
In a common One-Shot Signature service, an OTP (One-Time Password) code is sent by sms to the end user directly from Uanataca services. The OTP verification is used to activate the issuing of single-use digital signature certificate and the usage of it to sign the signature request documents.
<br></br>
One-Shot Signature can use other external authentication methods instead of Uanataca SMS. This alternative methods are subjected to approval.
<br></br>
The following images summarize One-Shot Signature flow involving both authentication methods:
</div>
<br></br>

> Uanataca SMS

![img](https://github.com/UANATACA/ONESHOT-REPO/raw/main/img/oneshot_flc1.png)

</br>

1. The business application creates a new digital signature request, providing all required user data
2. One-Shot Optimizer returns an identifier for the certificate request
3. The business application provides the documents to be signed by the end user
4. The business application retrieve the service contract
5. The business application shows the documents to be signed and the service contract to its end user
6. After reviewing the documents, the end user agrees to sign them
7. The business application starts the signature process by requesting the generation of a One-Time Password (OTP) token for the signature
8. Uanataca services sends the OTP directly to the end user through an SMS message
9. By introducing the OTP, the end user identifies himself as the subject of the signature certificate
10. The business application provides the OTP and the identifier of the signature request to the One-Shot Optimizer
11. One-Shot Optimizer takes care of computing the hash of the documents to be signed in the business layer
12. Hashes are sent together with the request identifier and OTP code to Uanataca Services
13. The end user signature certificate is generated and used to sign the hashes
14. The signed hashes and the signature identifier are returned to the One-Shot Optimizer
15. One-Shot Optimizer generates the signed document envelopment, combining the original documents with the signed hashes
16. Finallly, the business application calls One-Shot Optimizer API to obtain the signed documents
<br></br>

> Other authentication methods


![img](https://github.com/UANATACA/ONESHOT-REPO/raw/main/img/oneshot_flc2.png)

</br>

1. The business application creates a new digital signature request, providing all required user data
2. One-Shot Optimizer returns an identifier for the certificate request
3. The business application provides the documents to be signed by the end user
4. The business application retrieve the service contract
5. The business application shows the documents to be signed and the service contract to its end user
6. After reviewing the documents, the end user agrees to sign them
7. The client application starts the signature process with an authentication method provided by the client
8. One-Shot Optimizer takes care of computing the hash of the documents to be signed in the business layer
9. Hashes are sent together with the request identifier and an id of the busuness authentication method to Uanataca Services
10. The end user signature certificate is generated and used to sign the hashes
11. The signed hashes and the signature identifier are returned to the One-Shot Optimizer
12. One-Shot Optimizer generates the signed document envelopment, combining the original documents with the signed hashes
13. Finallly, the business application calls One-Shot Optimizer API to obtain the signed documents


# Test Environment

For testing purposes, we provide integrators of our pre-configured One-Shot Optimizer test environment accessible at the following URL:

</br>

	https://one-shot.developers.uanataca.com

</br>

In the same way, you can find the instructions to set up your own One-Shot Optimizer in the <a href="#section/Configuration"> configuration section</a>.


# Configuration

One-Shot Optimizer can be supplied as a **Docker** or as a **Virtual Machine** image.
See the configuration description in:<br>
<a href="#section/Configuration/One-Shot-Optimizer-on-Docker"> One-Shot Optimizer on Docker</a><br>
<a href="#section/Configuration/One-Shot-Optimizer-on-Virtual-Machine-(OVA)"> One-Shot Optimizer on Virtual Machine</a>


## Hardware requirements


**CPU:** modern multicore (minimum 4 core)

**RAM:** 8GB

**HDD:** 200 GB


## One-Shot Optimizer on Docker


This configuration requires a server with a Linux CentOS operating system.

<a href="#section/Video-tutorials/Docker-Optimizer-Configuration"><img src="https://raw.githubusercontent.com/UANATACA/ONESHOT-REPO/main/img4.png"></a><a href="#section/Video-tutorials/Docker-Optimizer-Configuration"><b>&nbsp;Watch on video!</b></a>


> STEP 1: Install Docker and Docker-Compose.

*Docker*

Run the following commands in this order.

	sudo yum update -y
	yum install -y yum-utils device-mapper-persistent-data lvm2
	yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
	sudo yum install -y docker-ce docker-ce-cli containerd.io
	sudo systemctl start docker



*Docker-Compose*

Run the following commands in this order.


	sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
	chmod +x /usr/local/bin/docker-compose


Run command **docker-compose version** to check the installation. The outcome should show this information:


![img](https://github.com/UANATACA/ONESHOT-REPO/raw/main/img/oneshot-docker1.png)

</br>

> STEP 2: Extract and copy One-Shot Optimizer zip content to the server.

Extract all `oneshot_optimizer_docker.zip` content in a local folder.

Move One-Shot Optimizer folder to the path **/opt** in the server.

The outcome should look like this:

![img](https://github.com/UANATACA/ONESHOT-REPO/raw/main/img/oneshot-docker2.png)


</br>

> STEP 3: Mapping volumes (for environments with a pool of One-Shot Optimizer).

In high performance environments with a pool of One-Shot Optimizer, service settings, data and logs must be stored in a shared volume outside Optimizer servers. These volumes must be defined in `docker-compose.yml` file in each One-Shot Optimizer.

	cd /opt/oneshot_optimizer

Docker-compose.yml settings file:

![img](https://github.com/UANATACA/ONESHOT-REPO/raw/main/img/oneshot-docker3.png)

</br>

> STEP 4: Load One-Shot Docker images.

Run the following commands:

	cd /opt/oneshot_optimizer
	docker image load -i oneshot_optimizer.tar
	docker image load -i oneshot_imgconverter.tar

Remove image files:

	rm -rf /opt/oneshot_optimizer/oneshot_optimizer.tar
	rm -rf /opt/oneshot_optimizer/oneshot_imgconverter.tar

</br>

> STEP 5: Launch the service.

Run the following commands:

	cd /opt/oneshot_optimizer
	docker-compose up -d

Check service status:

	docker-compose ps

					Name              			  Command               State                Ports
	--------------------------------------------------------------------------------------------------------------------------------------------------
	oneshot_optimizer_imgconverter_1   /opt/bit4id/imgconverter/b ...   Up      0.0.0.0:49153->5013/tcp,:::49153->5013/tcp
	oneshot_optimizer_nginx_1          /docker-entrypoint.sh ngin ...   Up      0.0.0.0:443->443/tcp,:::443->443/tcp, 0.0.0.0:80->80/tcp,:::80->80/tcp
	oneshot_optimizer_optimizer_1      oneshot_optimizer start          Up

All services must be UP.

</br>

> STEP 6: Service settings.

See <a href="#section/Configuration/Service-settings">service settings</a> configuration section.

</br>


## One-Shot Optimizer on Virtual Machine

<div style="text-align: justify">
The Virtual Machine is supplied in an OVA file. One-Shot Optimizer image is compatible with common virtual environments like VMWare, AWS, Azure or VirtualBox.
</div>
</br>

> STEP 1: Import One-Shot Optimizer (VM) in the virtual environment.

<div style="text-align: justify">
Adjust the system requirements for optimal usage considering host terminal resources described in <a href="#section/Configuration/Hardware-requirements"> hardware requirements</a>.
</div>

</br>

> STEP 2: Network configuration.

The network settings are configured on the file `ifcfg-ens33`, which can be found in the path **/etc/sysconfig/network-scripts**. Edit the file and insert the correct IP address, network mask, gateway and DNS for your network.

Then restart network services with command **service network restart**.

Example:

![img](https://github.com/UANATACA/ONESHOT-REPO/raw/main/img/oneshot-docker4.png)

</br>

> STEP 3: Service settings.

See <a href="#section/Configuration/Service-settings">service settings</a> configuration section.

</br>


## Service settings

<div style="text-align: justify">
One-Shot Signature can be configured to use in test or production environment.
</div>
<br></br>


> TEST environment

**Requirements:**

- Billing credentials for Uanataca test environment.

One-Shot Optimizer is already configured to use the Uanataca test environment. To start testing One-Shot Signature, it is enough to configure your Uanataca Billing account for test environment.

To do so, open the settings file `custom.ini` and insert the provided username and password under the [BILLING] section.

Custom.ini folder:

**/opt/oneshot_optimizer/common/etc/custom.ini** or custom mapped volume (Docker)

**/opt/bit4id/oneshot_optimizer/etc/custom.ini** (Virtual Machine)

**Password must be inserted in base64 format.** Run this command to convert your password to base64

	echo -n <<billing_password>> | base64

Custom.ini settings:

	1 | [BILLING]
	2 | USERNAME = billing-test-account@organization
	3 | PASSWORD = base64-password

Once you are done editing the file, restart the One-Shot Optimizer service to changes take effect.

Virtual Machine:

	systemctl restart optimizer

Docker:

	cd /opt/oneshot_optimizer
	docker-compose restart optimizer


<br></br>

> PRODUCTION environment

**Requirements:**

- Billing credentials for Uanataca production environment.
- Certificate (.cer) and key (.key) files to connect to the Uanataca production environment.
- The Id number for the Registration Authority that will issue the certificates.

<blockquote style="background-color: #faf3ac; border-color: #5a5a5a; color: #3b3b3b;">⚠ We recommend starting from a clean copy of One-Shot Optimizer for this step. This prevents leftover files from the test environment from causing errors in production.</blockquote>

You should have received a certificate (.cer) and key (.key) file to be used to identify your application in communications with the production signature service. Place both files in the certificates folder, replacing the certificates for the test environment present in the virtual machine.

**/opt/oneshot_optimizer/common/etc/certs** or custom mapped volume (Docker)

**/opt/bit4id/oneshot_optimizer/etc/certs** (Virtual Machine)

![img](https://github.com/UANATACA/ONESHOT-REPO/raw/main/img/oneshot-docker5.png)

Open the custom.ini file in /opt/bit4id/oneshot_optimizer/etc and configure it to interact with the production environment. The parts that you will likely need to change are listed below:

	1 | [ENV]
	2 | ENVIRONMENT = prod
	3 |
	4 | [TSA]
	5 | URL      = https://tsa.uanataca.com/tsa/tss03
	6 |
	7 | [BILLING]
	8 | USERNAME = example@uanataca.com
	9 | PASSWORD = my-password
	10|
	11| [RA]
	12| NO_REQUIRED_DOCUMENTS          = true
	13|
	14| DEFAULT_RA                     = 999
	15| DEFAULT_PROFILE                = PFnubeQAFCiudadano


Under [ENV] section, set environment to `prod`

[ENV]

 `ENVIRONMENT = prod`

Under the [BILLING] section, introduce the production Uanataca Billing credentials. **Password must be inserted in base64 format**. Run this command to convert your password to base64

	echo -n <<billing_password>> | base64

[BILLING]:

`USERNAME = billing-prod-account@organization`<br>
`PASSWORD = base64-password`

Under the [RA] section, make sure that the DEFAULT_RA matches your Registration Authority's identifer and the DEFAULT_PROFILE is set to the correct profile. Typically, this will be either `PFnubeQAFCiudadano` for EU eIDAS qualified certificates or `PFnubeNC` for non-qualified certificates.

[RA]:

`DEFAULT_RA = 999`<br>
`DEFAULT_PROFILE = PFnubeQAFCiudadano`


Once you are done editing the file, restart the One-Shot Optimizer service to changes take effect.

Virtual Machine:

	systemctl restart optimizer

Docker:

	cd /opt/oneshot_optimizer
	docker-compose restart optimizer

<br></br>


# Workflow 

This section presents the workflow for a simple use case of the One-Shot Signature service with a step-by-step description of the API calls required to allow a user to digitally sign a document provided by the client application. 

<a href="#section/Video-tutorials/Signature-Workflow-(SMS)"><img src="https://raw.githubusercontent.com/UANATACA/ONESHOT-REPO/main/img4.png"></a><a href="#section/Video-tutorials/Signature-Workflow-(SMS)"><b>&nbsp;Watch on video!</b></a>

The basic digital signature process involves the following steps:

- Retrieve an existing token for the RAO
- Create a new Digital Signature Request
- Upload a document
- Retrieve service contract
- Generate an OTP (only for Uanataca SMS)
- Sign the document
- Retrieve the signed document
- Delete documents from Optimizer


> STEP 1: Retrieve an existing token for the RAO

API reference: <a href="#tag/Tokens/paths/~1api~1v1~1tokens/get">List tokens</a>

The test One-Shot Optimizer is pre-configured with a Registration Authority Officer (RAO) account ready to be used within the test environment. This account has an associated token, that can be used to identify the RAO in API calls.

	curl -X GET https://one-shot.developers.uanataca.com/api/v1/tokens

On the clean machine, this should return a single token:

	1 | {
	2 |     "status": "200 OK",
	3 |     "details": {
	4 |         "6d1cae4d55be4cdf9cac50ee36f73406": {
	5 |             "username": "9001800",
	6 |             "password": true,
	7 |             "pin": true
	8 |         }
	9 |     }
	10| }

This output tells us that a single token "6d1cae4d55be4cdf9cac50ee36f73406" exists. This token is associated to the RAO account with id "9001800" and can be used in place of the password and pin.

To use tokens in a production environment, you will need to create them first with the corresponding <a href="#tag/Tokens/paths/~1api~1v1~1token/post">Create token</a> API call.
</br>

> STEP 2: Create a new Digital Signature Request

API reference: <a href="#tag/Requests/paths/~1api~1v1~1request/post">Create request</a>

Within the One-Shot Signature Service, all data pertaining to a given digital signature is collected within a Digital Signature Request. This includes both the identifying information of the signing user, which is provided when you create the signature request, and the document or documents to be signed, which we will upload later.

This call must include enough information to identify both the signing user and the RAO approving the request. The full description of the arguments accepted by this endpoint can be found in the API call detailed documentation, but for now it is enough to include at least the following:

	1 | curl --location --request POST 'https://one-shot.developers.uanataca.com/api/v1/request' \
	2 |      --form 'token=6d1cae4d55be4cdf9cac50ee36f73406' \
	3 |      --form 'profile=PFnubeQAFCiudadano' \
	4 |      --form 'given_name=name_of_the_user' \
	5 |      --form 'surname_1=surname_of_the_user' \
	6 |      --form 'email=user-example@domain.com' \
	7 |      --form 'mobile_phone_number=+343391234567' \
	8 |      --form 'document_front=@document_front.png' \
	9 |      --form 'document_rear=@document_rear.png' \
	10|      --form 'document_owner=@document_owner.png'

where token is the token representing the RAO credentials obtained in the previous step.

If the signature request is completed successfully, we will get the unique identifier assigned to it:

	1 | {
	2 |     "status": "201 Created",
	3 |     "details": 1464
	4 | }

The request code will be used to identify this digital signature request in subsequent calls.
</br>

> STEP 3: Upload a document

API reference: <a href="#tag/Documents/paths/~1api~1v1~1document~1{pk}/post">Upload document</a>


After creating the digital signature request, we can associate to it all pdf documents that should be signed by the user.

	curl -F "file=@doc.pdf" -X POST https://one-shot.developers.uanataca.com/api/v1/document/1464

Note that the number at the end of the call is the request id we obtained in the previous step.

If the upload is successful, the response will contain the identifier assigned to each document:

	1 | {
	2 |     "status": "200 OK",
	3 |     "details": "712c29ac-a2dc-4530-8c67-d0f227d8294b"
	4 | }

</br>

> STEP 4: Retrieve service contract

API reference: <a href="#tag/Documents/paths/~1api~1v1~1document~1{pk}~1contract/get">Retrieve contract</a>

As a Trusted Service Provider, Uanataca must inform certificate applicants of the terms and conditions governing the issuance of certificates. 

A service contract is generated in each digital certificate issue. The user must view the service contract to sign later along with the documents to be signed in the signature request, using the one time certificate issued on the spot.

	curl -X GET https://one-shot.developers.uanataca.com/api/v1/document/1464/contract

The response by the server will be the service contract document file in binary format:

	1 | %PDF
	2 | ...

</br>

> STEP 5: Generate an OTP

API reference: <a href="#tag/Requests/paths/~1api~1v1~1otp~1{pk}/post">Generate OTP code</a>

<blockquote style="background-color: #faf3ac; border-color: #5a5a5a; color: #3b3b3b;">This step is only used for flows using Uanataca SMS.</blockquote>

Once the documents to be signed are ready, we need to generate a secure One-time password (OTP) that will allow the user to sign them. The OTP is generated by calling the otp endpoint and the resulting OTP is sent as an SMS message directly to the phone number we provided when creating the signature request.

When calling the OTP endpoint, provide the request identifier returned by the request endpoint:

	curl -X POST https://one-shot.developers.uanataca.com/api/v1/otp/1464

A successful call will look like this:

	1 | {
	2 |     "status": "200 OK",
	3 |     "details": "OTP generated"
	4 | }

With this call, an SMS with the secret code is sent to the mobile phone number associated to the signature request.
</br>

> STEP 6: Sign the document

API reference: <a href="#tag/Requests/paths/~1api~1v1~1sign~1{pk}/post">Sign</a>

In this step we are going to issue the digital signature certificate and sign all documents previously uploaded for the signature request.

Call the sign endpoint with the request id and json parameters containing the OTP:

	curl -d @params.json -H "Content-Type: application/json -X POST https://one-shot.developers.uanataca.com/api/v1/sign/1464

params.json for Uanataca SMS:

	1 | {
	2 |     "secret": "123456"
	3 | }

params.json for other authentication methods:

	1 | {
	2 |     "secret": "123456"
	3 |     "ext_unlock_type": "biometric"
	4 |     "ext_unlock_value": "12345678-12345678"
	5 | }

</br>

A successful call will result in the following response:

	1 | {
	2 |     "status": "200 OK",
	3 |     "details": "Documents correctly signed"
	4 | }

</br>

> STEP 7: Retrieve signed document

API reference: <a href="#tag/Documents/paths/~1api~1v1~1document~1{pk}~1{type}~1{uid}/get">Retrieve document</a>

Once the signature is done, the next step is getting the signed documents.

To do this, query with an HTTP GET request the endpoint /api/v1/document/{pk}/{type}/{uid}, where {pk} is the Request's unique identifier, {type} is the type of the document (it can be "original" for the uploaded document or "signed" for the digitally-signed version) and {uid} is the document unique identifier.

	curl -X GET https://one-shot.developers.uanataca.com/api/v1/document/1464/signed/712c29ac-a2dc-4530-8c67-d0f227d8294b

The response by the server will be the document in binary format:

	1 | %PDF
	2 | ...

</br>

> STEP 8: Delete documents from Optimizer

API reference: <a href="#tag/Documents/paths/~1api~1v1~1documents~1{pk}/delete">Delete all request documents</a>

<blockquote style="background-color: #faf3ac; border-color: #5a5a5a; color: #3b3b3b;">⚠ While the service will not delete uploaded files unless explicitly requested through an API call, it is <strong>strongly recommended</strong> that you backup any files that you want to preserve using an alternative system.</blockquote>

Delete all documents associated to an ended digital signature request.

	curl -X DELETE https://one-shot.developers.uanataca.com/api/v1/documents/1464


</br>



# Logs

Service logs file `optimizer.log` is stored in a local folder in One-Shot Optimizer.

Docker path:

**/opt/oneshot_optimizer/common/logs** or custom mapped volume

Virtual Machine path:

**/opt/bit4id/oneshot_optimizer/logs**



# Postman collection

A postman collection is available as a support for a quick start.<br>
It is only required to edit `host`variable in Postman environment with the IP or domain of One-Shot Optimizer.

<a href="https://cdn.bit4id.com/es/uanataca/public/oneshot/Uanataca_One-Shot_Postman.zip">One-Shot Postman collection download</a>


# Video tutorials

Need a better understanding of One-Shot API? Check the video tutorials below and follow step-by-step instructions! They will guarantee you use our API efficiently for the best experience in document signatures.

## Docker Optimizer Configuration

The Docker Optimizer configuration requires an One-Shot Optimizer image package and a server using Linux Operating System with Internet access. Please check our <a href="#section/Configuration/One-Shot-Optimizer-on-Docker">documentation</a>.<br></br>

<figure class="video_container">
  <iframe width="560" margin-left="500px" height="315" src="https://www.youtube.com/embed/amGfQeMZQBA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>

## Signature Workflow (SMS)

This tutorial covers the step-by-step <a href="#section/Workflow">workflow</a> for document signature using Uanataca's One-Shot service via SMS.<br></br>

<figure class="video_container">
	<iframe width="560" height="315" src="https://www.youtube.com/embed/-XxjUfgEPRw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>

## Signature Workflow (External Authentication)

This tutorial covers the step-by-step <a href="#section/Workflow">workflow</a> for document signature using Uanataca's One-Shot service via Exthernal Authentication. <br></br>

<figure class="video_container">
	<iframe width="560" height="315" src="https://www.youtube.com/embed/5w0sdhJ3y7I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>

## Signature Image Configuration

Using images in signatures is an optional feature. Learn how to set signature image parameters in our One-Shot API <a href="#tag/Requests/paths/~1api~1v1~1sign~1{pk}/post">sign</a> call.<br></br> 

<figure class="video_container">
	<iframe width="560" height="315" src="https://www.youtube.com/embed/YTDqwhBQZ5c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</figure>

<div id="APIReference" style="padding-top: 60px;"><h1>API Reference<h1></div>