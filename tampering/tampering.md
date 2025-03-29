# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

The potential vulnerabilities in insecure.ts lie in the fact that this file explicitley trusts
the variable "req.body.name" to include a alphanumeric string. 

2. Briefly explain how a malicious attacker can exploit them.

If the user happens to input code into "req.body.name" when they are supposed to input their name,
the code will be executued. The vulnerability is in the fact that the developer did not sanatize the
inputs placed into req.body.name. The server is executing code directly from what was received from the http requests, which could be malicous.

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?

Now, we sanatize the input which will be loaded into "req.body.name", in this case using escapeHTML() which will replace all possible occurneces of code with a string. Ideally there would be a middleware function that will be applied to any route that needs to be sanatized. This example targets a specefic type of attack.