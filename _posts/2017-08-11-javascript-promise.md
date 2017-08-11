---
layout: post
title: A Quick Demo of Javascript Promises
category: javascript
published: true
---

### Using fetch

```javascript
let username = 'mrkjlchvz';
let url      = 'https://api.github.com/users/' + username + '/repos';

fetch(url)
  .then(response => {
    console.log(response);
    return response.json();
  })
  .then(data => {
    console.log(data); // the actual API data (list of repositories)
  });
```

### Using fetch, but with error checking

The above code looks good but lacks an error checking mechanism. What if we provided a
github username that does not exist? What if the github API is down?

Error checking is an important part when working with promises. Javascript makes it easy to do 
this via the `.catch` callback.

Using our first example:

```javascript
fetch....
  .then....
  .then....
  .catch(error => {
    // send to error reporting service;
    // or maybe send an email;
    // or maybe just do nothing and show it to the console (bad example)
    console.error(error);
  });
```

### Writing your own Promises

```javascript
let employees = [
  { id: 1, name: 'mark', position: 'Web Developer' },
  { id: 2, name: 'billy', position: 'System Analyst' },
  { id: 3, name: 'mark', position: 'Chief Architect' },
  { id: 4, name: 'christopher', position: 'Mobile Developer' },
];

function getEmployeeByName(name) {
  // return a Promise object
  return new Promise((resolve, reject) => {
    let employee = employees.find(emp => emp.name === name );

    if(employee) {
      resolve(employee);
    } else {
      reject(Error('Employee not found'));
    }
  });
}

getEmployeeByName('mark')
  .then(data => {
    const { name, position } = data;
    console.log('Hello ' + name + ', your position is ' + position);
  })
```
