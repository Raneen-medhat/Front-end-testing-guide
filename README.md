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
 **Install Enzyme:**
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


----------------------------------------------------------------------------------------------------------------------------

# Test Cases Examples
  Here’s a simple App that takes any input from user and prints it in front of him. It also brings some data of users from     an API (“https://jsonplaceholder.typicode.com/users”).

  ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image4.png)


  ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image1.png)


 **Here’s the code section:**

  ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image3.png)


## 1 - "Input field is required" test case: 
  **Test Case Target:** if user didn’t fill the input field he will get validation message

   1 -  Wrap the App component to see data in it.
   2 -  check that the attribute "required"  is there.

   ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image2.png)





## 2 - "check that minimum length of input is 5" test case: 
   **Test Case Target:** If user fills the input field with less than 5 char he would get a validation message.

  1 - find the input field 
  2 - check it has the attribute minLength  = “5”

  ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image6.png)





## 3 - "Check that when input is null when submitted" test case: 
   **Test Case Target:** the input field does not submit empty value.
  
  1 - find the input field 

  2 - simulate the value of input field with “ ” which means null

  3 - find the button 

  4 - simulate the click action on button 

  5 - Should pop up the required attribute

 ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image5.png)





## 4 - "check that state is updated with input value when submitted" test case: 
   **Test Case Target:** update state with input value.

  1 - find the input field.

  2 - simulate the input field with value “ merna ”.

  3 - simulate the button click.

  4 - setState with value “ merna ”.

  5 - check that the state.name is equal to “ merna ”.

 ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image8.png)


  **Another Way**

 ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image2.png)





## 5 - "check that “ real api ” returns status code of 200" test case: 
   **Test Case Target:** check that api is valid and returns response.


  ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image7.png)

  1 - instance() is a function that returns all the data inside a component including any data outside the render function
  2 - fire the postData function

  3 - check that status returned from function fire equals to 200 which means api was successfully called and returned users       data 

  **Below you can see other test cases examples from another app**

  ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image9.png)






## 6 - "check that api has been called one time" test case: 
   **Test Case Target:** check api is called one time.

  ```sh
    it(‘api has been called one time’, () => {
    const spy = jest.spyOn(api, "fetchSearchResult");
    expect(spy).toHaveBeenCalledTimes(1)
  })
 ```





## 7 - "Check that api has been called" test case: 
   **Test Case Target:** check that api is valid and returns response.

   **Note:** 
     This case  has the same target of Fifth case test but here we test url not method, 
     Using mockAxios.get:   for mocking axios get method
     We assume searchValue to equal react, then mock axios get method.

  ```sh
    import mockAxios from ‘axios’;
    it(‘api has been called’, () => {
    const searchValue = "react";
    expect(mockAxios.get).toHaveBeenCalledWith(
          https://www.googleapis.com/books/v1/volumes?q=${searchValue}`,
     );
      }) 
      })
    })
   ```





## 8 - "Check that user filled input field,  then user clicked on search button, and the api has been called" test case: 
   **Test Case Target:** response return from api after click on the search button with specific search value.

  **SearchBar component:**

  
  ```sh
      import React from "react";
      import { onFetchSearchResult } from "../store/actions/";
      import { connect } from "react-redux";

      class SearchBar extends React.Component {
        constructor(props) {
          super(props);
        }
         state = {
          searchBox: ""
        };
       getSearchResult = (value, e) => {
          e.preventDefault();
          this.props.onFetchSearchResult(value);
        };

        handleChange = e => {
          return this.setState({ searchBox: e.target.value });
        };

        render() {
          console.log(this.state.searchBox, this.props.searchResult);
          return (
            <div className="container">
              <nav className="navbar navbar-light bg-light">
                <form
                  className="form-inline"
                  onSubmit={e => {
                    this.getSearchResult(this.state.searchBox, e);
                  }}
                >
                  <input
                  id='searchInput'
                    className="form-control mr-sm-2"
                    type="search"
                    placeholder="Search"
                    aria-label="Search"
                    onChange={this.handleChange}
                    value={this.state.searchBox}
                  />
                  <button
                    className="btn btn-outline-success my-2 my-sm-0"
                    type="submit"
                  >
                    Search
                  </button>
                </form>
              </nav>
            </div>
          );
        }
      }
   ```


  **Note:**
    In this app we use react-redux for store, so  we need to mock store to complete the test case, so you can ask me how to     mock store?!

   1 - install redux-mock-store library via command :
     
  ```sh
     npm i --save redux-mock-store
  })
 ```

   2 - import configureStore from 'redux-mock-store' . 
   3 - put configureStore in variable.
        
  ```sh
     npm i --save redux-mock-store
 ```
  Then set initialState

  ```sh
      Const initialState = {};
 ```
                    
  4 - In describe run mockStore in beforeEach() method -you can use this method if you want to run anything before each it         part in one describe-   store =mockStore(initialState).
  5 - You should add store in each component you want to test.

   ```sh
    mount(<SearchBar store={store} />).
    const initialState = {};
    const mockStore = configureStore();
    let store, container;
    describe("User filled input field ,then clicked submit, and api return         with response", () => {
    beforeEach(() => {
      store = mockStore(initialState);
    });
 
    it("search value should be found, api has been called", () => {
      const container = mount(<SearchBar store={store} />)
      const form = container.find("form");
      const input = form.find("input");
      const wrapper = container.find("SearchBar");
      wrapper.instance().setState({ searchBox: "merna" });
 
      expect(wrapper.instance().state.searchBox).toBe("merna");
 
      const inputValue = input.simulate("change", 
                             { target: { value:"react books" } });
      const item = input.instance().value;
      expect(item).toBe("react books");
 
      const button = container.find(‘button’).simulate(‘click’)
 
      const spy = jest.spyOn(api, "fetchSearchResult");
      expect(spy).toHaveBeenCalledTimes(1);
    });
  });
  ```






## 9 - "Check that  response return from api in special format" test case: 
   **Test Case Target:** response return as an object.

  1 - Fire “fetchSearchResult” 
  2 - expect response to equal special format

   ```sh
     it("Response return from api", () => {
     api.fetchSearchResult().then(response => {
     expect(response).toEqual( {"data": {}});
    });  
   });
 ```






## 10 - "Check that  action is firing" test case: 
   **Test Case Target:** some action is firing.

  **The action creator**
   ```sh
     it("Response return from api", () => {
     api.fetchSearchResult().then(response => {
     expect(response).toEqual( {"data": {}});
    });  
   });
 ```

  ![alt text](https://github.com/Raneen-medhat/Front-end-testing-guide/blob/master/image10.png)

 **Applying test for it**

  1 -  assign “dummy” value to a constant
  2 - create an action creator that takes action type and action payload
  3 - test that “onFetchSearchResult” is the same format as the action creator we assumed in our test

   ```sh
    describe("actions", () => {
    it("create action to call saga", () => {
    const searchValue = "text";
    const actionCreator = { type: FETCH_SEARCH_RESULT_SAGA, searchValue };
    expect(onFetchSearchResult(searchValue)).toEqual(actionCreator);
    });
   });
 ```

----------------------------------------------------------------------------------------------------------------------------

# Errors
### If case you face errors like these, you can apply these steps to resolve it:


  **## Error:** 
  **Add @babel/plugin-proposal-class-properties (https://git.io/vb4SL) to the 'plugins' section of your Babel config to         enable transformation"**

  **## Solve:**
    **1 - Install this libraryL**

     ```sh
      npm install --save-dev @babel/plugin-proposal-class-properties
     ```

   **2 - Add to babel.config.js file this line**

     ```sh
       Module.experts = {
        plugins : [
         [ “@babel/plugin-proposal-class-properties”]
        ],
        }
     ```





  **## Error:** 
    **ReferenceError: regeneratorRuntime is not defined**

   **## Solve:**
      **in bable.config.js add in plugins:**

   ```sh
       plugins: [
      ["@babel/plugin-proposal-class-properties"],
      ["@babel/transform-runtime"]
        ]
   ```





  **## Error:** 
    **For testing real API If you use the GET method in your component and don't get any response**

   **## Solve:**
      **you must return the result 
        Example: return axios.get(“..............”)**
