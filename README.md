# Front-end testing guide

## In This Documentation We Will Talk about :

  - ### Introduction to testing.
    - Why we are using testing 
    - Types of Tests
    - What about jest
    - What about Enzyme
    - Why we use Enzyme with Jest

  - ### Jest and Enzyme Installation.
    - Jest Configuration
    - Enzyme Configuration
    
  - ### Test Cases Examples.
    - Test Cases
    - Resolve Errors


------------------------------------------------------------------------------------------------------------------------------

##  Introduction to testing

  ### 1 - Why we are using testing ?
  Testing the internal implementation of an object is always a bad idea. This holds true for React, JavaScript, and for any       programming language out there. What we can do instead is testing the component by keeping in mind what the user should see. 
  A functional test, or End to End test is a way of testing web applications from the user’s perspective.We are testing the       component from the user’s point of view.
  So we use testing to make sure that our application is act as we suppose used by end user.

 ### 2 - Types of Tests
   - ### End To End.
     Testing full blown user flows in the browser.
     These tests consist of minimal mocks (i.e — you really are spinning up all the services that the user would be using).
     
   - ### Integration
     Testing interactions between multiple services / components.
     An “Integration test” is a bloated and often ambiguous term. For example, setting up a test that verifies interactions        between multiple services (e.g — an api and a database) has overhead associated with it that is close to writing a full      blown E2E test. On the other hand, writing a test that multiple react components work together in a redux environment        has the complexity that is closer to a unit test. Read on to find out why ).

   - ### Unit 
     Testing a single component / function in isolation.
     A unit test is essentially testing input and output. It doesn’t get easier to reason about than this.


     ### Some other types of testing:
      - **Manual :  A human being actually going through and verifying a flow on a real device.**
      - **Snapshot: Verifying a component’s rendered output.**
      - **Static:   Testing pre compile-time (ESLint, TypeScript).**
      for more Information about testing types  : [Read this article](https://itnext.io/react-redux-integration-tests-with-jest-enzyme-df9aa6effd13).

