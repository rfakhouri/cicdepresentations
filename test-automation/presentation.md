# Test Automation

---

End to End Tests

---

Why are they important?

Note: Codifies business logic, ensures code changes don't break that.

---

Who should write them?

Note: Question for audience

---

Who writes them in your department?

Note: Question for audience

---

Do you see any issues with that?

Note: Question for audience

---

Who do I think should write them?  

Developers and (Product) Development Team

---

What do you need to run them

---

Tech Options

---

Cypress.io

Note: Chrome based system only (Chrome/Chromium/Electron)

------

Selenium

Note: Multibrowser requires another framework

------

Pupeteer

Note: Chrome only requires another framework

------

Cucumber

Note: 

------

Appium

Note: Mobile App Development

---

Unit Tests

---

Are they necessary?

Note: It depends. 

------

Maybe...  

It really depends. 


------

Can you run your entire system in a PR?  

Can you run all of your End to End tests in a PR?

------

If the answer to either of those is yes then probably not. 

Note: E2E tests can ensure correctness of your application

------

Are you developing an Open Source Library or Framework?

------

If the answer to that question is yes then you absolutely need them. 

Note: A stable contract is very important, you don't want to break things for your users.

---

Test Structure

------

Tests both unit and end to end follow the same structure: 

0. Setup test
0. Run test
0. Verify test

---

Tests require testable code

------

Nicely Unit Testable Code

-------

Inject Dependencies

------

Bad Tightly Coupled Code :(

```js
function Foo() { 
  var dbConnection;
  var results = dbConnection.doSomething();
  
  /*
    Lots of processing stuff here
  */
 
 return processedResults;
}

```

------

Nice Loosely Coupled Code :)

```js
function Foo(dbConnection) { 
  var results = dbConnection.doSomething();
  
  /*
    Lots of processing stuff here
  */
 
 return processedResults;
}

```
------

Reduce Side Effects

Note: Functions should do one thing and preferably it should 

---

Nicely Testable Web Apps

------

ID's

Just throw these on everything.

---

Most Importantly write your own tests, you won't make your stuff testable if you don't feel the pain.
