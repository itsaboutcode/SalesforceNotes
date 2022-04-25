- [Apex Programming Language](#apex-programming-language)
  - [Writing Apex](#writing-apex)
  - [Apex Triggers](#apex-triggers)
  - [Asynchronous Apex](#asynchronous-apex)
  - [Debugging Apex](#debugging-apex)
  - [Testing Apex](#testing-apex)
    - [Code Coverage Requirement for Deployment](#code-coverage-requirement-for-deployment)
      - [What's Code Coverage](#whats-code-coverage)
      - [Deployment Requirement](#deployment-requirement)
    - [What to Test in Apex](#what-to-test-in-apex)
    - [Accessing Private Test Class Members](#accessing-private-test-class-members)
    - [Example Test Syntax](#example-test-syntax)
    - [Steps to Apex Testing From Developer Console](#steps-to-apex-testing-from-developer-console)
    - [Apex Testing in VS Code](#apex-testing-in-vs-code)
    - [Create and Execute a Test Suite](#create-and-execute-a-test-suite)
    - [Testing Apex Triggers](#testing-apex-triggers)
    - [Create Test Data for Apex Tests](#create-test-data-for-apex-tests)
    - [Testing Call Outs (REST/HTTP and SOAP)](#testing-call-outs-resthttp-and-soap)
      - [SOAP Call Outs Testing](#soap-call-outs-testing)
        - [Steps to Test SOAP Call Outs](#steps-to-test-soap-call-outs)
          - [Step # 01](#step--01)
          - [Step # 02](#step--02)
          - [Step # 03](#step--03)
      - [REST Call Outs Testing](#rest-call-outs-testing)
        - [Step # 01](#step--01-1)
        - [Step # 02](#step--02-1)
      - [Multiple Call outs in One Test](#multiple-call-outs-in-one-test)
- [Reference](#reference)


# Apex Programming Language

- Apex is a `strongly typed`, object-oriented programming language.
- It allows developers to execute `flow and transaction control statements` on the Salesforce Platform server.
- Apex code can only be written in a `sandbox environment or a Developer org`, not in production. 
- Apex code can be deployed to a production org from a sandbox.

## [Writing Apex](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode/apex_writing.htm)

[Trailhead | Build Apex Coding Skills](https://trailhead.salesforce.com/en/content/learn/trails/build-apex-coding-skills)

## [Apex Triggers](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode/apex_triggers.htm)

[Trailhead | Apex Triggers](https://trailhead.salesforce.com/en/content/learn/modules/apex_triggers)

## [Asynchronous Apex](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode/apex_async_overview.htm)

[Trailhead | Asynchronous Apex](https://trailhead.salesforce.com/content/learn/modules/asynchronous_apex)


## [Debugging Apex](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode/apex_debugging.htm)

[Trailhead | Find and Fix Bugs with Apex Replay Debugger](https://trailhead.salesforce.com/en/content/learn/projects/find-and-fix-bugs-with-apex-replay-debugger)


## [Testing Apex](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode/apex_testing.htm)

- You can write and execute test cases for your classes and triggers with Apex testing framework on lightning platform.
- Apex unit tests and code coverage of minimum 75% are requirements for deploying and distributing Apex.

> Before each major service upgrade, Salesforce runs all Apex tests on your behalf through a process called `Apex Hammer`. The Hammer process runs in the current version and next release and compares the test results. This process ensures that the behavior in your custom code hasn’t been altered as a result of service upgrades. The Hammer process picks orgs selectively and doesn’t run in all orgs. Issues found are triaged based on certain criteria. Salesforce strives to fix all issues found before each new release.

### Code Coverage Requirement for Deployment

#### What's Code Coverage

This metric shows the number of `code lines` executed during test case execution, Nothing else!

```js
average = (number of lines executed by test cases)/(total numer of line) * 100%
```

- Blue lines covered by test cases
- Red lines are **not** covered by test cases.

![test-coverage1](https://user-images.githubusercontent.com/204423/164885878-63860c45-73f6-40a0-81a3-793f2422f10b.png)


#### Deployment Requirement

Before you can deploy your code or package it for the Salesforce AppExchange, the following must be true.

- Unit tests must `cover` at least 75% of your Apex code, and all of those tests must complete successfully.
- Every trigger must have some test coverage.
- All classes and triggers must compile successfully.

### [What to Test in Apex](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_testing_what.htm)

- Single Actions
  - Test to verify that a single record produces the correct, expected result.
- Bulk Actions
  - Any Apex code, whether a trigger, a class or an extension, may be invoked for 1 to 200 records. 
  - You must test not only the single record case, but the bulk cases as well.
- Positive Behavior
  - Test to verify that the expected behavior occurs through every expected permutation, that is, that the user filled out everything correctly and did not go past the limits.
- Negative Behavior
  - There are likely limits to your applications, such as not being able to add a future date, not being able to specify a negative amount, and so on. 
  - You must test for the negative case and verify that the error messages are correctly produced as well as for the positive, within the limits cases.
- Restricted User
  - Test whether a user with restricted access to the sObjects used in your code sees the expected behavior.
  - That is, whether they can run the code or receive error messages.


### [Accessing Private Test Class Members](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_testing_testvisible.htm)

If you want to test private/protected `members (methods, variables, classes)`, you have 2 options

1. Make a public method which uses private members.
2. Annotate private/protected members of a class with `@TestVisible` so that you can access them from your test class and use those members.


### Example Test Syntax

- Test `classes` can be either private or public. 
- If you’re using a test class for unit testing only, declare it as `private`. 
- Public test classes are typically used for test data factory classes.
- Test `methods` must be defined in test classes, which are classes annotated with `isTest`.
- The `visibility` of a test method doesn’t matter, so declaring a test method as public or private doesn’t make a difference as the testing framework is always able to access test methods. 
- For this reason, the access modifiers are omitted in the syntax.
- Declare method as `static`.

```js
@isTest
private class MyTestClass {
    @isTest static void myTest() {
        System.assertEquals('Expected Value',
                            'Actual Value', 
                            'Failed Message');
    }
}
```

- The verifications are done by calling the `System.assertEquals()` method, which takes two parameters: the first is the expected value, and the second is the actual value. 
- There is another version of this method that takes a third parameter—a string that describes the comparison being done.
-  This optional string is logged if the assertion fails.

### Steps to Apex Testing From Developer Console

1. In the Developer Console, click `File -> New -> Apex Class`, and enter the class name e.g; `TestTemperatureConverter` for the class name, and then click OK.
2. Annotate class and it's methods with `@isTest`
3. In the Developer Console, click `Test -> New Run`
4. Under Test Classes, select your class, e.g; `TestTemperatureConverter`.
5. To add all the test methods in the `TestTemperatureConverter` class to the test run, click **Add Selected**.
6. Click **Run**.
7. In the `Tests tab`, you see the status of your tests as they’re running. Expand the test run, and expand again until you see the list of individual tests that were run. They all have green checkmarks. 

![test-result](https://user-images.githubusercontent.com/204423/164886232-053e798b-30cd-45e9-a68b-f4562369077b.png)

After you run tests, code coverage is automatically generated for the Apex classes and triggers in the org. You can check the code coverage percentage in the Tests tab of the Developer Console.

![test-coverage](https://user-images.githubusercontent.com/204423/164886240-a2dcce08-3cab-485d-bfb6-4f4dd7e22be0.png)


While one test method would have resulted in full coverage of the class in question, it’s still important to test for different inputs to ensure the quality of your code.

### [Apex Testing in VS Code](https://developer.salesforce.com/tools/vscode/en/apex/testing)

### Create and Execute a Test Suite

### [Testing Apex Triggers](https://trailhead.salesforce.com/en/content/learn/modules/apex_testing/apex_testing_triggers)

- Triggers are tested by firing the trigger and verify expected results.
- To isolate the data setup process’s limit usage, enclose the test call within the [Test.startTest() and Test.stopTest() block](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_testing_tools_start_stop_test.htm)


### [Create Test Data for Apex Tests](https://trailhead.salesforce.com/content/learn/modules/apex_testing/apex_testing_data)

- The `TestDataFactory` class is a special type of class—it is a public class that is annotated with isTest and can be accessed only from a running test.
- Test utility classes contain methods that can be called by test methods to perform useful tasks, such as setting up test data. 
- Test utility classes are excluded from the org’s code size limit.

### Testing Call Outs (REST/HTTP and SOAP)

- By default, test methods don’t support SOAP and REST callouts, and tests that perform web service callouts fail.

#### SOAP Call Outs Testing

- For `SOAP`, Apex provides the built-in `WebServiceMock` interface and the `Test.setMock` method. 
- Use `WebServiceMock` and `Test.setMock` to `receive fake responses` in a test method.

- WSDL2Apex auto-generated class call `WebServiceCallout.invoke`, which performs the callout to the external service.
- When testing these methods, you can instruct the Apex runtime to `generate a fake response` whenever `WebServiceCallout.invoke` is called.
- To do so, implement the `WebServiceMock interface` and specify a `fake response` for the Apex runtime to send.

##### [Steps to Test SOAP Call Outs](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_callouts_wsdl2apex_testing.htm)

###### Step # 01

- First, implement the` WebServiceMock` interface and specify the fake response in the `doInvoke` method.
- The class implementing the WebServiceMock interface can be either `global or public.`
- You can annotate this class with @isTest because it is used only in a test context. In this way, you can exclude it from your org’s code size limit of 6 MB.

```js
@isTest
global class CalculatorCalloutMock implements WebServiceMock {
   global void doInvoke(
           Object stub,
           Object request,
           Map<String, Object> response,
           String endpoint,
           String soapAction,
           String requestName,
           String responseNS,
           String responseName,
           String responseType) {
        // start - specify the response you want to send
        calculatorServices.doAddResponse response_x = 
            new calculatorServices.doAddResponse();
        response_x.return_x = 3.0;
        // end
        response.put('response_x', response_x); 
   }
}
```

###### Step # 02

- Call the service.

```js
public class AwesomeCalculator {
    public static Double add(Double x, Double y) {
        calculatorServices.CalculatorImplPort calculator = 
            new calculatorServices.CalculatorImplPort();
        return calculator.doAdd(x,y);
    }
}
```

###### Step # 03

- Now that you have specified the values of the fake response, instruct the Apex runtime to send this fake response by calling `Test.setMock` in your test method. 
- For the first argument, pass `WebServiceMock.class`, and for the second argument, pass a new instance of your interface implementation of `WebServiceMock`.
- After this point, if a web service callout is invoked in test context, the callout is not made. You receive the mock response specified in your doInvoke method implementation.


```js
@isTest
private class AwesomeCalculatorTest {
    @isTest static void testCallout() {              
        // This causes a fake response to be generated
        Test.setMock(WebServiceMock.class, new CalculatorCalloutMock());
        // Call the method that invokes a callout
        Double x = 1.0;
        Double y = 2.0;
        Double result = AwesomeCalculator.add(x, y);
        // Verify that a fake result is returned
        System.assertEquals(3.0, result); 
    }
}
```

#### REST Call Outs Testing
- For `REST`, Apex provides the built-in `HttpCalloutMock` interface to specify the response sent in the respond method, which the Apex runtime calls to send a response for a callout.

##### Step # 01
- First, implement the `HttpCalloutMock` interface and specify the fake response in the `response` method.
- The class implementing the `HttpCalloutMock` interface can be either `global or public.`
- You can annotate this class with @isTest because it is used only in a test context. In this way, you can exclude it from your org’s code size limit of 6 MB.

```js
@isTest
global class AnimalsHttpCalloutMock implements HttpCalloutMock {
    // Implement this interface method
    global HTTPResponse respond(HTTPRequest request) {
        // Create a fake response
        HttpResponse response = new HttpResponse();
        response.setHeader('Content-Type', 'application/json');
        response.setBody('{"animals": ["majestic badger", "fluffy bunny", "scary bear", "chicken", "mighty moose"]}');
        response.setStatusCode(200);
        return response; 
    }
}
```

##### Step # 02

- Call the method which have REST callout and provide the mock response before executing the method

```js
@isTest 
static void testPostCallout() {
    // Set mock callout class 
    Test.setMock(HttpCalloutMock.class, new AnimalsHttpCalloutMock()); 
    // This causes a fake response to be sent
    // from the class that implements HttpCalloutMock. 
    HttpResponse response = AnimalsCallouts.makePostCallout();
    // Verify that the response received contains fake values
    String contentType = response.getHeader('Content-Type');
    System.assert(contentType == 'application/json');
    String actualValue = response.getBody();
    System.debug(response.getBody());
    String expectedValue = '{"animals": ["majestic badger", "fluffy bunny", "scary bear", "chicken", "mighty moose"]}';
    System.assertEquals(expectedValue, actualValue);
    System.assertEquals(200, response.getStatusCode());
}
```

#### [Multiple Call outs in One Test](https://salesforce.stackexchange.com/questions/139235/how-to-create-mock-class-for-multiple-callouts-in-single-class)

- It's possible that you have to make multiple callouts in one test method. To provide mock response, following code will do the trick.
- And even if you don't have multiple requests in one test method, below code is good approach to provide response in one file for multiple use cases.

```js
private class Mock implements HttpCalloutMock {
        public HTTPResponse respond(HTTPRequest req) {
            if (req.getEndpoint().endsWith('abc')) {
                HTTPResponse res = new HTTPResponse();
                res.setBody('{}');
                res.setStatusCode(200);
                return res;
            } else if (req.getEndpoint().endsWith('xyz')) {
                ...
            } else {
                System.assert(false, 'unexpected endpoint ' + req.getEndpoint());
                return null;
            }
        }
    }
```

And you can use it like any other mock.

```js
@IsTest
    static void abc() {
        Test.setMock(HttpCalloutMock.class, new Mock());
        ...
    }

    @IsTest
    static void xyz() {
        Test.setMock(HttpCalloutMock.class, new Mock());
        ...
    }
```


# Reference

- [Apex Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode)
- [Enhance Salesforce with Code](https://help.salesforce.com/s/articleView?id=sf.extend_code_overview.htm&type=5)
- [Apex Reference Guide](https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_ref_guide.htm)
- [Trailhead Specialist | Apex Spcialist](https://trailhead.salesforce.com/en/content/learn/superbadges/superbadge_apex)
- [Trailhead Specialist | Data Integration Specialist](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_integration)
- [Trailhead Specialist | Advanced Apex Specialist](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_aap)
- [Trailhead Trail | Build Apex Coding Skills](https://trailhead.salesforce.com/en/content/learn/trails/build-apex-coding-skills)
- [Trailhead | Apex Testing](https://trailhead.salesforce.com/content/learn/modules/apex_testing)
- [Testing HTTP Callouts](https://developer.salesforce.com/docs/atlas.en-us.224.0.apexcode.meta/apexcode/apex_classes_restful_http_testing_httpcalloutmock.htm)
