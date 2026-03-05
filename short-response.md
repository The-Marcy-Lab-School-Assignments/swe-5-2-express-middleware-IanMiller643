# Short Response Questions

Answer each question below in your own words. Aim for 3–5 sentences per answer. Be specific — use the exact terms and concepts from the lesson.

Your responses will each be evaluated out of 6 points. You can earn 3 points for writing quality and 3 points for the accuracy and precision of the technical content per question.

---

## Question 1: Express vs `node:http`

Express is described as a framework that "wraps" `node:http`. What does that mean? Compare how you would handle a `GET /api/users` request in `node:http` versus in Express. What does Express do for you automatically that you had to write manually with `node:http`?

**Your answer here**:

Express is described as a framework that "wraps" `node:http` because it does the same thing as the module, but it allows us to avoid writing redundant boilerplate code.

Express 
```js
const express = require('express');
const app = express();

const getUsers = (req, res, next) => {
    res.send(users);
}

app.get('/api/users', getUsers);
```

node:http
```js
const http = require('node:http');

const server = http.createServer((req, res) => {
    const { path, method } = req;

    if (method === 'GET' && path === '/api/users') {
        res.writeHead(200, {'Content-Type': 'application/json'});
        res.end(JSON.stringify(users));
        return;
    }

});
```

In the two code snippets above, we're making a get request to our api's endpoint with both express and `node:http`. In `node:http`, have to invoke the `res.writeHead()` method to set the status code and write te headers for the response. Then we have to invoke `res.end()` to send the response that was converted into a string using `JSON.stringify()`. In express, this is simplified with the `res.send()` method that handles all of that logic.

---

## Question 2: Endpoints, Controllers, and Middleware

What are **controllers** and **middleware** in Express? What are each responsible for and how do they work together to handle incoming requests?

**Your answer here**:

In express, **controllers** are callback functions that read a request and handle the response to it. **Middleware** on the other hand are also callback functions, but they handle logic between the request and response cycle. An example of controllers and middleware working with together to handle requests would be when logging the request's method, url, and time that it was made. Middleware would handle this logic, pass the request onto the next controller using `next()`, invoke the`app.use()` method so that every request will be logged, and finally send the request with one of the controllers.

---

## Question 3: Query Strings and Route Parameters

How are **query strings** and **route parameters** similar? How are they different? In your answer, provide an example of when you would use each.

**Your answer here**:

**Query strings** and **route parameters** are similar because they both allow the user to input characters into the url to change what data they receive from an endpoint. They are different in that a route parameter is used to receive a specific piece of data while query parameters are used for filtering or modifying the data that is received. For example, if an endpoint had an array of user objects, we could use a query parameter to only get users who are adults. If each user had an id, we would use a route parameter to get that specific user.

---

## Question 4: Same-Origin Requests

For API fetch calls from a client-side application, explain the difference between fetching from endpoints with relative paths like `/api/quotes` and fetching from endpoints with a full URL like `https://dog.ceo/api/breeds/image/random`. Why do we not send a fetch using a url like `http://localhost:8080/api/quotes`?

**Your answer here**:

