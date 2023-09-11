# Firebase Cheat Sheet

### Fnstall firebase bakage
```bash
npm i firebase
```

### Inishialize firebase app
```js
import { initializeApp } from 'firebase/app';

// TODO: Replace the following with your app's Firebase project configuration
const app = initializeApp({
  //...
});
```
> **NOTE:** the firebase configuration object is berfectly safe to inclode in the *client side*
>
> it's how the firebase librari knows how it talks to your firebase project
>
> **Security** are maintained in security rules and app check in the firebase

### Firebase services
#### Authantication
```js
import { initializeApp } from 'firebase/app';
import { getAuth, onAuthStateChanged } from 'firebase/auth';
// Follow this pattern to import other Firebase services
// import { } from 'firebase/<service>';

// TODO: Replace the following with your app's Firebase project configuration
const app = initializeApp({
  //...
});

// before using any services you must initialize the app first
const auth = getAuth(app);

// Detect auth state
onAuthStateChanged(auth, user => {
  if (user != null) {
    console.log("user logged in!")
  } else {
    console.log("no user...")
  }
})
```
### Firestore
```js
import { initializeApp } from 'firebase/app';
import { getFirestore, collection, getDocs } from 'firebase/firestore/lite';
// Follow this pattern to import other Firebase services
// import { } from 'firebase/<service>';

// TODO: Replace the following with your app's Firebase project configuration
const app = initializeApp({
  //...
});

// before using any services you must initialize the app first
const db = getFirestore(app);

// create a collection
// collection(<getFirestore function>, <collectin name>)
const todosCol = collection(db, "todos")

// get documents
// await getDocs(<collectin name>)
const snapshot = await getDocs(todosCol)

// Get a list of cities from your database
async function getCities(db) {
  const citiesCol = collection(db, 'cities');
  const citySnapshot = await getDocs(citiesCol);
  const cityList = citySnapshot.docs.map(doc => doc.data());
  return cityList;
}
```
# Firebase Hosting
After building the react progect
```bash
npm run build
```
## Firebase CLI setup
### install <in node_modules>
```bash
npm i firebase-tools -D
```
### firebase login
```bash
// new login
node_modules/.bin/firebase login
// login with another account
node_modules/.bin/firebase login:add another@email.com
// to switch between account
node_modules/.bin/firebase login:use another@email.com
```
### init hosting
```bash
node_modules/.bin/firebase init hosting
```
then process with Wizzard
```bash
// 1
Are you ready to proceed? (Y/n) y
// 2
Please select an option: (Use arrow keys)
> Use an existing project 
  Create a new project
  Add Firebase to an existing Google Cloud Platform project
  Don\'t set up a default project
// 3
Select a default Firebase project for this directory: (Use arrow keys)
> project-1 (name) 
  project-2 (name) 
  project-3 (name)
// 4
 What do you want to use as your public directory? (public)
// 5
Configure as a single-page app (rewrite all urls to /index.html)? (y/N) y
// 6
Set up automatic builds and deploys with GitHub? (y/N) y
// 7
File public/index.html already exists. Overwrite? (y/N) n
// 8
For which GitHub repository would you like to set up a GitHub workflow? (format:        
user/repository)
// 9
Set up the workflow to run a build script before every deploy? (y/N) y
// 10
What script should be run before every deploy? (npm ci && npm run build)
// 11
Set up automatic deployment to your site\'s live channel when a PR is merged? (Y/n) y
// 12
What is the name of the GitHub branch associated with your site\'s live channel? (master)
```
Firebase initialization is complete!

## Firebase Deploy
to avoid deploying for other things such as "Firebase functions", provide `--only hosting` flag
```bash
node_modules/.bin/firebase deploy --only hosting
```
---
Resource

[Firebase Doc](https://firebase.google.com/docs/web/setup?continue=https%3A%2F%2Ffirebase.google.com%2Flearn%2Fpathways%2Ffirebase-web%3Fhl%3Den%23article-https%3A%2F%2Ffirebase.google.com%2Fdocs%2Fweb%2Fsetup)
[Getting started with Firebase Hosting (and GitHub Actions!)](https://youtu.be/P0x0LmiknJc?si=XpdVhbjOwlhhacc_)
