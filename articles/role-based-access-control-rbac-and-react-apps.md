## Role based access control and react apps

### Introduction
* Authorization is a process in which developers control the access to information by users and also limit the actions users can perform
* An authenticated user is a user who has identified themselves somehow
* A solid authorization system has to:
  * Limit the AJAX requests performed
  * Deny access to certain client-side routes
  * Display or hide certain pieces of UI
* Please refer to the [original article](https://auth0.com/blog/role-based-access-control-rbac-and-react-apps/) 

### Authentication in React Apps with Auth0
* Assigning Roles to Users with Auth0
* Integrating Auth0 in your React App
  * create an `authContext` using React Context API in `authContext.js`
  * create an `Auth` component that will provide its children access to `authContext` in `Auth.js`
    * login
      ```
      initiateLogin = () => auth.authorize();
      ```
    * call `handleAuthentication()` when callback and parse the result and `setState()` to set the session information
    * `logout()` to reset the role to `visitor`
    * create a `Callback` component in `callback.js`
    * create a `Login` and `Logout` component
    * update `Home` component to enable user login    

### Handling Authorization in React Apps: the Naive Way
* Flaws
  * When requirements change, you will have to check every condition related to authorization
  * For each new role added, the whole codebase has to be modified
  * The code is imperative
  * Code duplication

### Role-Based Access Control: a Better Solution
* Advantages
  * All the permissions are at one place
  * Creating new roles is very easy
  * Favors declarative programming 
* Role-Based Access Control Example
  * create `rbac-rules.js` to contain all the rules with `resource:action` format
  * Implementing the `Can` Component which takes the rules and decides whether users can perform the desired action or see some part of the UI
  * Using the `Can` component to protect the other components with roles and perform