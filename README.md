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


 ### 3 - What about jest
   Jest is a JavaScript unit testing framework, used by Facebook to test services and React Apps, Jest acts as a test runner,    assertion library, and mocking library.

   Jest also provides **Snapshot testing**:
   ### Snapshottests: 
   are a very useful tool whenever you want to make sure your UI does not change unexpectedly.A typical snapshot test case      for a mobile app renders a UI component, takes a snapshot, then compares it to a reference snapshot file stored alongside    the test. The test will fail if the two snapshots do not match: either the change is unexpected, or the reference snapshot    needs to be updated to the new version of the UI component.

  **Fortunately,** the Jest testing framework has simplified a lot of the complexities behind testing. The secret is a tool     called a **mock**. A mock is effectively a shortened version of a function. Instead of running the function you stub out     theresult you want. Your code will return what you want instead of running the live code.
  In other words, you say what an API should return. The mock will bypass the live API and return the data directly. Instead   of relying on a date function that changes every 24 hours, you effectively freeze it in place by returning the same date     every time.
  a mock is just replacing a live piece of code with a simple function that returns the data you expect.


 ### There are two ways to mock functions: Either by creating a mock function to use in test code, or writing a manual mock        to override a module dependency.
   Ex:
```sh
   Mock function:const myMock = jest.fn();
   Manual mock: const mockCallback = jest.fn(x => 42 + x);
   Mock Module: jest.mock('axios')
```
 [Read more about mock](https://ponyfoo.com/articles/disguise-driven-testing-jest-mocks-in-depth).

 [Read more about mock in Jest Doc](https://jestjs.io/docs/en/mock-functions).


 ### Creating a test file
   - Jest will look for tests in any of the following places:
   - Files with .js suffix in __tests__ folders.
   - Files with .test.js suffix.
   - Files with .spec.js suffix.


 ### 4 - What about Enzyme
  Enzyme is a JavaScript Testing utility for React that makes it easier to assert, manipulate, and traverse your React         Components’ output.
  Enzyme, created by Airbnb, adds some great additional utility methods for rendering a component (or multiple components),     finding elements, and interacting with elements.
  Summary of all methods in Enzyme.


  ### 5 - Why we use Enzyme with Jest
  Both Jest and Enzyme are specifically designed to test React applications, Jest can be used with any other Javascript app     but Enzyme only works with React.
  Jest can be used without Enzyme to render components and test with snapshots, Enzyme simply adds additional functionality.
  Enzyme can be used without Jest, however Enzyme must be paired with another test runner if Jest is not used.
  As described, we will use:
  **Jest** as the test runner, assertion library, and mocking library.
  **Enzyme** to provide additional testing utilities to interact with elements.


----------------------------------------------------------------------------------------------------------------------------
## Jest and Enzyme Installation
   ### - Jest Configuration
   After create your app using **creat-react-app**
   1 - remove App.test.js
   2 - Install Jest: npm install --dev jest babel-jest @babel/preset-env @babel/preset-react react-test-renderer
   [Jest Configuration](https://jestjs.io/docs/en/tutorial-react).

   3 - in **package.json** file 
  ```sh
  "scripts": {
      "test": "jest"
    }
```
  4 - create file with name **babel.config.js**  in the same level like **(public and src).** 
      Ex: 
      - public
      - src
      - babel.config.js

  5 - in **bable.config.js** write these lines:
  ```sh
    module.exports = {
      presets: ['@babel/preset-env', '@babel/preset-react'],
    };
    }
```
 6 - To make sure your jest config is successfully
    - create a new folder called __tests__ in your src folder because by default jest looks for __tests__ folder in your           project and runs all tests present inside that folder.
    **Update App.js with :**

  ```sh
  import React, { Component } from 'react';
 
  class App extends Component {
    render() {
      return (
        <div className="App">
          <button>Show</button>
        </div>
      );
     }
   } 
    export default App;
    }
```

  **create a new file called App.test.js in your __tests__ folder.**
  ```sh
      import React from 'react';
      import App from '../App';
      import { create } from 'react-test-renderer'

      describe('My first snapshot test',()=>{
          test('testing app button', () => {
          let tree = create(<App />)
          expect(tree.toJSON()).toMatchSnapshot();
        })
      });
 ```

 **Run in your cmd**
   ```sh
   npm test
 ```

 **Note:**
  To watch to every change, add this line in package.json
  ```sh
     "scripts": {
        "test": "jest",
        "test:watch": "npm run test -- --watch"
    }
 ```
**And run this command**
  ```sh
   npm run test -- --watch
 ```

 **If you update any thing in component, you should run this command.**
   ```sh
   npm test -- --updateSnapshot
 ```

----------------------------------------------------------------------------------------------------------------------------

# Enzyme Configuration
 ** Install Enzyme:**
  ```sh
   npm install --save-dev enzyme enzyme-adapter-react-16 enzyme-to-json
 ```

 - Create a setupTests.js file at ./src/setupTests.js and write in it:
  ```sh
   import { configure } from 'enzyme';
   import Adapter from 'enzyme-adapter-react-16';
   configure({ adapter: new Adapter() });
 ```
  [Read More About Testing React with Jest and Enzyme](https://medium.com/codeclan/testing-react-with-jest-and-enzyme-20505fec4675).




