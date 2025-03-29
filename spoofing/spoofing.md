# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.

In insecure.ts, the session secret is a hardcoded string. This makes it easier for a malicous user to get access to another user's session ID. Also, it is missing some secure flags which make it harder for malicous users to steal cookies or perform other spoofing related attacks. 

2. Briefly explain different ways in which vulnerability can be exploited.

One way this vulnerability can be exploited is through session hijacking. A malicous user can use an html page to steal another users cookies, and impersonate them. Also, there is the potential of a csrf attack. In this case, an html can be used to forces users to execute an unwanted action.

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.

In secure.ts, the session secret is not a hardcoded string. Also, httpOnly is set to truem secure is set to true, and sameSite is set to true which make it harder to steal the cookies fom another user. ALso csrf tokens are implemnted to verify request authenticiy and therefore prevent against csrf attacks.