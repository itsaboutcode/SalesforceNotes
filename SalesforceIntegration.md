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

### Authorize Endpoint

- In Salesforce, before making any request to an external API, we need to authorize it. Otherwise we will get following error.

`System.CalloutException: Unauthorized endpoint, please check Setup->Security->Remote site settings. endpoint = https://api.spoonacular.com/recipes/random`

<img width="617" alt="Screenshot 2022-03-31 at 11 16 25 AM" src="https://user-images.githubusercontent.com/204423/160989008-67946867-72bc-4526-95f3-293f6f6a255e.png">


# Terminologies

### OpenAPI

- An api for which you don't need to authorize yourself to make the call. [Spoonacular](https://spoonacular.com/food-api/docs) is one such example.

# Reference

- [Apex Integration Services](https://trailhead.salesforce.com/en/content/learn/modules/apex_integration_services)
- [Data Integration Specialist](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_integration)
- [APEX + Integration](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode/apex_running.htm)
- [SFDCFacts Academy | Salesforce Integration Crash Course | The Ultimate Guide to Salesforce Integrations | In 100 Minutes](https://www.youtube.com/watch?v=2myol9hI28c&t=1269s)
