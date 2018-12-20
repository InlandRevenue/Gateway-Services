![IRD logo](../../Images/IRlogo.gif)
![Software Dev](../../Images/SoftwareDev.png)

Resident withholding tax (RWT) Software Development Kit (SDK) for Investment Income Reporting
=======================================

Key Features:
-------------

- Simulating RWT filing operations
    - [Message samples](#message-samples-) - positive responses
	- [Requests Matching Logic](#requests-matching-logic)
	
- Business use cases
	- [view on IR website](https://www.ird.govt.nz/resources/xxx/III-RWT-business-use-cases-worked-examples.pdf)
	
- Schemas and WSDLS
	- View and download the [common xsd](../../Schema%20-%20Common/)
	- View and download the [return service Investment Income common xsd](../../Service%20-%20Return/Latest/)
	- View and download the RWT return [xsd](ReturnRWT.v1.xsd) and [wsdl](ReturnsRWTDevWsdl.wsdl) from this current directory
	
- Returns Service - Investment Income Information 
	- [Download the build pack](../../Service%20-%20Return/Latest/Gateway%20Services%20Build%20Pack%20-%20Return%20Service.pdf) to view data definitions of each operation and response status code definitions
	
- Identity and Access Services
	- [How to Integrate with OAuth](../../Service%20-%20Identity%20and%20Access/Latest/OAuth%20Authentication%20-%20How%20to%20Integrate.md)
	- [Sample curl commands](../../Service%20-%20Identity%20and%20Access/Latest/OAuth%20Authentication%20-%20How%20to%20Integrate.md) - for testing the OAuth flow
	- [Message Samples](../../Service%20-%20Identity%20and%20Access/Latest/) - OAuth requests and responses
	- [Download the build pack](../../Service%20-%20Identity%20and%20Access/Latest/Build%20pack%20-%20Identity%20and%20Access%20Services.pdf) - for OAuth 2.0 implementation   

      Message samples :
-----------------

- Simulating RWT Returns Operations:
    - File
        - Positive response
            - [request sample](sample%20messages/body-rwt-returnfile-request.xml)
            - [response sample](sample%20messages/body-rwt-returnfile-response.xml)
    - RetrieveStatus
        - Positive response
            - [request sample](sample%20messages/body-rwt-returnstatus-request.xml)
            - [response sample](sample%20messages/body-rwt-returnstatus-response.xml)
    - RetrieveReturn
        - Positive response
            - [request sample](sample%20messages/body-rwt-retrievereturn-request.xml)
            - [response sample](sample%20messages/body-rwt-retrievereturn-response.xml)

            
Requests Matching Logic
-----------------------

- ReadMe Page - (default) port 8080 of root path of Welcome Page
- Authentication mappings - (default) port 8443 of following paths:
    - /ms_oauth/oauth2/endpoints/oauthservice/authorize
    - /oam/server/auth_cred_submit
    - /ms_oauth/oauth2/endpoints/oauthservice/tokens
- Returns Service Mappings - (default) port 8080 of path "/gateway/GWS/Returns":
    - /gateway/GWS/Returns?wsdl - wsdl is not available, returning http 200 only
    - /gateway/GWS/Returns - Authentication validation will be performed at first:
        - if fail then return Authentication Errors
        - if pass then:
            - XML validation will be performed:
                - if fail then return XML Validation Errors
                - if pass then return positive responses
- Default Mapping - Very last matching logic to handle all other requests by returning 404 error when no matching found