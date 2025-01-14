<a href="https://www.vipm.io/package/pantherlab_lib_firebase_api/"> <img src="https://www.vipm.io/package/pantherlab_lib_firebase_api/badge.svg?metric=installs"></a> <a href="https://www.vipm.io/package/pantherlab_lib_firebase_api/"><img src="https://www.vipm.io/package/pantherlab_lib_firebase_api/badge.svg?metric=stars"></a>

# firebase-api

## How to create  a firebase project:

1. go to https://firebase.google.com/
2. Click  the button  "Get Started"
3. Click  the button "Add Project"
4. Add a project  Name
5. Disable "Enable Google Analytics for this project" checkbox and click "Create project"
6. Create a new Real Time Database <br><img src="assets/realTimeDB.png" width="60%" height="60%">
7. Click  The Button  "Create Database"
![image](https://github.com/PantherLAB/Firebase/assets/5545396/0fd69ed4-872c-42f7-8af2-3fa4158c386a)

8. Select the desired Location and click "Next"
9. Select "Start in Test Mode" and click Enable <br><img src="assets/testMode.png" width="80%" height="80%">
10. Locate the DB URL and the rules editor This is the "Firebase URL" to be used by the API <br><img src="assets/databaseURL.png" width="50%" height="50%">

## How to enable Authentication:

1. Select Authentication and click "Get Started"
![image](https://github.com/PantherLAB/Firebase/assets/5545396/23b28bea-c3d7-4a26-baac-e35543ac3c88)


2. Select Sign-in method tab and click the "Email/Password" Button and then click "Save" Button <br><img src="assets/SignInProviders.png" width="80%" height="80%">
3. Go to the Project Overview (click the gear button) and select "Project Settings", find the Web "API_Key" <br><img src="assets/webAPIkey.png" width="80%" height="80%">


## Using Firebase API

### Autenticate a new User

Open Sign In Example.vi and update the "API_KEY" and "Firebase URL" with the ones obtained in the previous steps <br><img src="assets/SignUPFirebase.png" width="90%" height="90%">

This Example will add your USER to the autenticated Users list <br><img src="assets/AutenticatedUserList.png" width="90%" height="90%">

### Post to Real Time DB

Open Log in and Post.vi Example, use your "API_KEY", "Firebase URL" and your Authenticated user to POST something to your Real Time Database, in this example we published a cluster called data, data is the endPoint name <br><img src="assets/logInPost.png" width="90%" height="90%">

### Editing your Rules

Until this point your Real Time Database is open to any autenticated user, we can create rules to match our neads, for example, if this database is meant to be used by a company we can create rules to allow reading and/or writting for an specific domain<br><img src="assets/rules.png" width="90%" height="90%">

Rules Example 1, allow writting and reading from specific domain  users:<br>
```
{
  "rules": {
    ".read": "auth.token.email.endsWith('@domain.com')",  
    ".write": "auth.token.email.endsWith('@domain.com')",  
  }
}
```
Rules Example 2, allow writting and reading from specific domain and filtering enabled to search under data/date
```
{
  "rules": {
    "data" : {
                ".indexOn": ["date"]
            },
     ".read": "auth.token.email.endsWith('@domain.com')",  
     ".write": "auth.token.email.endsWith('@domain.com')",  
    
  }
}
```
After you instal the VIPM Package there is an example provided for you, just drag it into your Block diagram and test it after setup your Firebase Database.

Rules Example 3,what actually worked for the example. from chat GPT
```
{
  "rules": {
    ".read": "auth != null", // only authenticated users can read
    ".write": "auth != null", // only authenticated users can write
    "log": {
      ".indexOn": ["date"]
    }
  }
}
```

Example what Data should look like after POST. Make sure your rules .indexOn arguement and endpoint match these fields. 
![image](https://github.com/joshball26/Firebase/assets/77031830/3654777f-c6f7-45b2-a588-9a7b4aa967b1)

## TroubleShooting 
If you get error 5001 saying you need to add a .indexOn to your firebase rules. you may need to authenticate the email address you are using to login 
- try testing your credentials in the rules playground tool on the WEB ![image](https://github.com/joshball26/Firebase/assets/77031830/a00da60a-71e2-4f44-97a1-f26b1fbf7556)

For more rules examples go to:<br>
https://medium.com/@juliomacr/10-firebase-realtime-database-rule-templates-d4894a118a98<br>
https://firebase.google.com/docs/rules<br>

[![Watch the Tutorial](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e1/Logo_of_YouTube_%282015-2017%29.svg/2560px-Logo_of_YouTube_%282015-2017%29.svg.png)](https://youtu.be/vDQ-mFWDiUk)
