# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.

The main vulnerability in insecure.ts comes from the the way in which the "userinfo" endpoint takes user input and directly queries the mongodb databse. This input is not sanatized, so if a user inputs a nosql query, it can be used to query the database in malicous ways. Additionaly, if the user sends a query for an invalid id, this can crash the server. 

2. Briefly explain how a malicious attacker can exploit them.

If the user sends an invalid id to be queried in the server, the server might crash or throw an error. Additionaly, a user can query the database many times in quick succession which can cause the server to crash.


3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?

 One way the secure.ts defends against the dos attack is a rate limiter. There is a rate limiting middleware function which will only allow a client to send a request once every five seconds. Also there is a try-catch block which prevents the server from crashing. 
