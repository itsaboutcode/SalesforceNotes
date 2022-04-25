- [Salesforce Integration Guide/Notes](#salesforce-integration-guidenotes)
  - [Web Services](#web-services)
    - [REST](#rest)
    - [SOAP](#soap)
    - [REST Web Service Methods](#rest-web-service-methods)
  - [Making Request To External Service](#making-request-to-external-service)
    - [Example REST Callout](#example-rest-callout)
    - [Making Request Using Developer Console](#making-request-using-developer-console)
    - [Authorize Endpoint](#authorize-endpoint)
    - [Example SOAP Callout Using WSDL](#example-soap-callout-using-wsdl)
      - [WSDL](#wsdl)
      - [SOAP](#soap-1)
      - [Real life analogy to WSDL and SOAP.](#real-life-analogy-to-wsdl-and-soap)
    - [Generating Proxy files using WSDL document](#generating-proxy-files-using-wsdl-document)
    - [Example SOAP Callout Using HTTP](#example-soap-callout-using-http)
  - [Expose Your Apex Class as a Web Service](#expose-your-apex-class-as-a-web-service)
    - [Example Use Case](#example-use-case)
    - [Steps to Expose a Class as a REST Service](#steps-to-expose-a-class-as-a-rest-service)
    - [Steps to Expose a Class as a SOAP Service](#steps-to-expose-a-class-as-a-soap-service)
    - [Test Your Apex REST Class](#test-your-apex-rest-class)
  - [Terminologies](#terminologies)
- [Reference](#reference)

# Salesforce Integration Guide/Notes

- It's needed when we need to connect 2 or more different systems e.g; if you wanted to show your dropbox files in your salesforce org page.


![UKHzcELU](https://user-images.githubusercontent.com/204423/160611269-3b723fde-7e73-4cf5-992c-edf00ecc0131.png)

## Web Services

### REST
- Fast
- Supports all type of devices.
- Works with JSON, XML and other formats.

### SOAP
- Slow (compared to REST).
- Works with XML.
- More secure in comparision than REST.
- Mostly used in Enterprise Applications.
- You get a document called `WSDL`, which have all the information about request and response of any given service. It help you created request and response classes and methods with parser (in most cases). In-case of REST, you don't have any such faciltiy.

### REST Web Service Methods

- GET - Retrieve the records.
- POST - Insert the records.
- PUT - Insert new records or update existing records.
- PATCH - Update existing records.
- Delete - Delete existing records.

## Making Request To External Service

### Example REST Callout

```java
// Since we are making call over http, we need an instanace of HTTP.
Http http = new Http();

// We also need an instance of HttpRequest, which we will send over http using HTTP instance.
HttpRequest request = new HttpRequest();

// Now we ware adding the information related to request e.g; Endpoint we are hitting and type of request it's. In this case it's GET.
request.setEndpoint('https://th-apex-http-callout.herokuapp.com/animals');
request.setMethod('GET');

// Here we make a request and expect a response in HttpResponse instance.
HttpResponse response = http.send(request);

// If the request is successful (status code is 200), parse the JSON response.
if(response.getStatusCode() == 200) {
    
    // Deserialize the JSON string into collections of primitive data types.
    Map<String, Object> results = (Map<String, Object>) JSON.deserializeUntyped(response.getBody());
    
    // Cast the values in the 'animals' key as a list
    List<Object> animals = (List<Object>) results.get('animals');
    
    System.debug('Received the following animals:');
    for(Object animal: animals) {
        System.debug(animal);
    }
}
```

### Making Request Using Developer Console

- You can run the above code in developer console. Go to developer console, and from there, click on `Debug` -> `Open Execute Anonymous Window`

<img width="306" alt="developer-console" src="https://user-images.githubusercontent.com/204423/160990237-294dc233-f336-4bcd-9277-5a75b0c44f80.png">

<img width="642" alt="debug_window" src="https://user-images.githubusercontent.com/204423/160990399-54743a34-d29c-479d-bf60-ac75c8833750.png">

- In `Anonymous Window`, you can execute the code by clicking the `Execute` button at the bottom of the screen

<img width="823" alt="Execute code" src="https://user-images.githubusercontent.com/204423/160990582-9c707c80-93d5-4d61-b749-ccb321dc2538.png">

### Authorize Endpoint

- In Salesforce, before making any request to an external API, we need to authorize it. Otherwise we will get following error.

`System.CalloutException: Unauthorized endpoint, please check Setup->Security->Remote site settings. endpoint = https://api.spoonacular.com/recipes/random`

<img width="617" alt="Unauthorized Endpoint Error" src="https://user-images.githubusercontent.com/204423/160989008-67946867-72bc-4526-95f3-293f6f6a255e.png">

- Now to make request, you need to add your site in **Remote site settings**. You can go there by visiting `Setup->Security->Remote Site Settings`

<img width="1426" alt="Remote Site Settings" src="https://user-images.githubusercontent.com/204423/160991942-3c73d9ec-f11e-43dd-8d9f-d132a5a3bf89.png">

<img width="1420" alt="Add URL FORM" src="https://user-images.githubusercontent.com/204423/160992447-fe32835d-a434-43b4-bce3-7088f21ea29f.png">

### Example SOAP Callout Using WSDL

#### WSDL

- A **WSDL** is an **XML document** that **describes** a web service. 
- It tells about the functions that you can implement or exposed to the client e.g; getRecipe etc, request parameters, which are optional, which are required etc and also about the response.
- It actually stands for **Web Services Description/Definition Language**.

#### SOAP

- **SOAP** is an **XML-based protocol** that lets you **exchange info** over a particular protocol (can be HTTP or SMTP, for example) between applications. 
- It stands for **Simple Object Access Protocol** and uses XML for its messaging format to relay the information.

#### Real life analogy to WSDL and SOAP.

**WSDL:** When we go to a restaurant we see the **Menu Items**, those are the WSDL's

**Proxy Classes:** Now after seeing the Menu Items we make up our Mind. So, basically we make Proxy classes based on WSDL Document.

**SOAP:** Then when we actually order the food based on the Menu's. Meaning we use proxy classes to call upon the service methods which is done using SOAP.

### Generating Proxy files using WSDL document

You can create Apex classes using `WSDL` file but it's no different than making request to REST base call in terms of code. In the body of request, you will have to send XML in SOAP protocol and in response, you should expect XML in SOAP protocol.

- Go to `Setup -> Apex Classes -> Generate from WSDL`

<img width="1404" alt="WSDL Apex File Generator" src="https://user-images.githubusercontent.com/204423/161012515-e459cbf7-9e38-4154-8e0c-bb3579f037e0.png">

- Select the WSDL file and click `Parse WSDL`

<img width="1173" alt="Select WSDL File" src="https://user-images.githubusercontent.com/204423/161051062-41d578bc-a410-4f1b-aa9f-08f6314dfecf.png">

- Now you will show the classes extracted from WSDL file. You get the opportinuty to change the name of classes before classes are created.

<img width="1155" alt="Classes Extrated" src="https://user-images.githubusercontent.com/204423/161051368-cea9ab37-0d88-4867-95a9-03e3ea89a9f6.png">

- For each generated class, a second class is created with the same name and the prefix `Async`. The `CalculatorServices` class is for synchronous callouts. The `AsyncCalculatorServices` class is for asynchronous callouts. 

<img width="1165" alt="Final output" src="https://user-images.githubusercontent.com/204423/161051285-db185b94-dfa8-4234-9018-f4c9da9d3c9a.png">

### Example SOAP Callout Using HTTP

```js
        HttpRequest req = new HttpRequest();
        req.setMethod('POST');
        req.setEndpoint('https://th-apex-http-callout.herokuapp.com/animals.asmx');
        req.setHeader('Content-Type', 'text/xml; charset=UTF-8');
        req.setHeader('SOAPAction', 'SomeAction');
        req.setHeader('Content-Length', '0');
        req.setBody('<?xml version="1.0" encoding="utf-8"?>' +
            + '<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">'
            + '<soap:Body xmlns="">'
            + '</soap:Body></soap:Envelope>');

            System.debug('Request =' + req.getBody().unescapeXml());

            Http http = new Http();
            HttpResponse res = http.send(req);

```

## [Expose Your Apex Class as a Web Service](https://trailhead.salesforce.com/en/content/learn/modules/apex_integration_services/apex_integration_webservices)

- You can expose your Apex class methods as a `REST or SOAP` web service operation.
- By making your methods callable through the web, external applications can integrate with Salesforce.

### Example Use Case
- You hav an internal app used to make calls to potential leads.
- You can show the leads data from Salesforce in your app and also get updates in the lead status, if any.

### [Steps to Expose a Class as a REST Service](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_rest.htm)

1.  Define your class as `global`.
2.  Define methods as `global static`.
3.  Add annotations to the class (@RestResource(urlMapping='/Account/*')) and methods (@HttpGet)

```js
@RestResource(urlMapping='/Account/*')
global with sharing class MyRestResource {
    @HttpGet
    global static Account getRecord() {
        // Add your code
    }
}
```

- The base endpoint for Apex REST is https://yourInstance.my.salesforce.com/services/apexrest/.
- The URL mapping is appended to the base endpoint to form the endpoint for your REST service (https://yourInstance.my.salesforce.com/services/apexrest/Account/*)
- The URL mapping is case-sensitive and can contain a wildcard character (*).

The following method annotations are available. 



### [Steps to Expose a Class as a SOAP Service](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_web_services.htm)

1.  Define your class as `global`.
2.  Add the `webservice` keyword and the `static` definition modifier to each method you want to expose. 
3.  The `webservice` keyword provides global access to the method it is added to.


```js
global with sharing class MySOAPWebService {
    webservice static Account getRecord(String id) {
        // Add your code
    }
}
```

- The external application can call your custom Apex methods as web service operations by consuming the class WSDL file.
- You can generate this WSDL for your class from the class detail page, accessed from the Apex Classes page in Setup.

### [Test Your Apex REST Class]()




## Terminologies 

- **OpenAPI:** An api for which you don't need to authorize yourself to make the call. [Spoonacular](https://spoonacular.com/food-api/docs) is one such example.
- Request
- Response
- Statuscode
- Endpoint
- Callout

# Reference

- [Trailhead | Apex Integration Services](https://trailhead.salesforce.com/en/content/learn/modules/apex_integration_services)
- [Trailhead | Data Integration Specialist](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_integration)
- [APEX + Integration](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode/apex_running.htm)
- [SFDCFacts Academy | Salesforce Integration Crash Course | The Ultimate Guide to Salesforce Integrations | In 100 Minutes](https://www.youtube.com/watch?v=2myol9hI28c&t=1269s)
- [Integration and Apex Utilities](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_integration_intro.htm)
- [Apex Rest](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_rest_intro.htm)
- [REST API Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.224.0.api_rest.meta/api_rest/intro_what_is_rest_api.htm)
- [APIs and Integration](https://developer.salesforce.com/developer-centers/integration-apis)
- [SFDC Panther+ | Salesforce Integration Tutorials](https://www.youtube.com/watch?v=Jcmw5WqjNwU&list=PLV3ll8m0ZlpqVOJCTFJu8uNJ-f2OppInR)
- [Salesforce Hulk | Understanding REST APIs and Integrations Basics in Salesforce Development](https://www.youtube.com/watch?v=mmS5V3j1E9U)
