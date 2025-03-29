# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

When the user enters their username, that string is inserted into "req.query". Then, this "query" value is converted into a mongodb object which will be used to execute the mongoose query. Once again, we are trusting user input without sanatizing it.

2. Briefly explain how a malicious attacker can exploit them.

A malicous attacker can explout this by inputing something like "$ne". In this case, the code will convert this input into a mongodb object which can be used to query the database in malicous ways, and potentially gain access to sensitive information.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?

This file sanatizes the input coming from the user into "req.query". In this case, we have written a regular expression to replace all alphanumeric characters with the empty string. Thus, the username cannot be interpreted as a mongodb object, and therfore can not be used to query the database and gain access to secure information.