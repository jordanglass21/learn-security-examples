# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

The 'update-role' function relies on attacker controller variables. That is, req.body.userId and req.body.newRole, which are defined by the user and responsile for their privlege level.

2. Briefly explain how a malicious attacker can exploit them.

A user can say they are an admin and downgrade the role of another user.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?

Rather than user imputing their IDs, the server can just read the IDs from the session itself. In this way we rely on a more secure mechanism to validate a user's ID. Please note, we should alter the cookie to set secure: true and not hardoce the secret in order o avoid a spoofing attack.