# Integration

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

### Rest Web Service Methods

- GET - Retrieve the records.
- POST - Insert the records.
- PUT - Insert new records or update existing records.
- PATCH - Update existing records.
- Delete - Delete existing records.

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

## Making Request Using Developer Console

- You can run the above code in developer console. Go to developer console, and from there, click on `Debug` -> `Open Execute Anonymous Window`

<img width="306" alt="developer-console" src="https://user-images.githubusercontent.com/204423/160990237-294dc233-f336-4bcd-9277-5a75b0c44f80.png">

<img width="642" alt="debug_window" src="https://user-images.githubusercontent.com/204423/160990399-54743a34-d29c-479d-bf60-ac75c8833750.png">

- In `Anonymous Window`, you can execute the code by clicking the `Execute` button at the bottom of the screen

<img width="823" alt="Execute code" src="https://user-images.githubusercontent.com/204423/160990582-9c707c80-93d5-4d61-b749-ccb321dc2538.png">

### Authorize Endpoint

- In Salesforce, before making any request to an external API, we need to authorize it. Otherwise we will get following error.

`System.CalloutException: Unauthorized endpoint, please check Setup->Security->Remote site settings. endpoint = https://api.spoonacular.com/recipes/random`

<img width="617" alt="Unauthorized Endpoint Error" src="https://user-images.githubusercontent.com/204423/160989008-67946867-72bc-4526-95f3-293f6f6a255e.png">


# Terminologies

### OpenAPI

- An api for which you don't need to authorize yourself to make the call. [Spoonacular](https://spoonacular.com/food-api/docs) is one such example.

# Reference

- [Apex Integration Services](https://trailhead.salesforce.com/en/content/learn/modules/apex_integration_services)
- [Data Integration Specialist](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_integration)
- [APEX + Integration](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode/apex_running.htm)
- [SFDCFacts Academy | Salesforce Integration Crash Course | The Ultimate Guide to Salesforce Integrations | In 100 Minutes](https://www.youtube.com/watch?v=2myol9hI28c&t=1269s)
