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

---
Resource

[Firebase Doc](https://firebase.google.com/docs/web/setup?continue=https%3A%2F%2Ffirebase.google.com%2Flearn%2Fpathways%2Ffirebase-web%3Fhl%3Den%23article-https%3A%2F%2Ffirebase.google.com%2Fdocs%2Fweb%2Fsetup)
