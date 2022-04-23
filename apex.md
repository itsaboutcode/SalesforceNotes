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
- If you’re using a test class for unit testing only, declare it as private. 
- Public test classes are typically used for test data factory classes.

- Test `methods` must be defined in test classes, which are classes annotated with `isTest`.
- The `visibility` of a test method doesn’t matter, so declaring a test method as public or private doesn’t make a difference as the testing framework is always able to access test methods. 
- For this reason, the access modifiers are omitted in the syntax.

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

[Trailhead | Apex Testing](https://trailhead.salesforce.com/content/learn/modules/apex_testing)




# Reference

- [Apex Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.234.0.apexcode.meta/apexcode)
- [Enhance Salesforce with Code](https://help.salesforce.com/s/articleView?id=sf.extend_code_overview.htm&type=5)
- [Apex Reference Guide](https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_ref_guide.htm)
- [Trailhead Specialist | Apex Spcialist](https://trailhead.salesforce.com/en/content/learn/superbadges/superbadge_apex)
- [Trailhead Specialist | Data Integration Specialist](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_integration)
- [Trailhead Specialist | Advanced Apex Specialist](https://trailhead.salesforce.com/content/learn/superbadges/superbadge_aap)
- [Trailhead Trail | Build Apex Coding Skills](https://trailhead.salesforce.com/en/content/learn/trails/build-apex-coding-skills)
