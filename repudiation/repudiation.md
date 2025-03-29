# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.

The issue here is there is no logging of the user's interaction with the server. If a user were to  perform malicious activities, then there would be no records to audit and figure out how the attack was performed. 

2. Briefly explain why the vulnerability is addressed in __secure.ts__.

There is a middlware function which will log every http request with the user and time the request was sent. Additionaly, we will log erros. We can then audit the logs and determine if there is a pattern causing these errors to occur.

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?

There are two design patterns in secure.ts which address the vulnerability. One is the use of the middleware pattern. The middleware intercepts each http request and logs information regarding each request, such as time and user. Also we have the observer pattern. The code server.log acts as an observer, reacting to http requests and errors, and is resposible for loging the actual information using logStream.write(). 
