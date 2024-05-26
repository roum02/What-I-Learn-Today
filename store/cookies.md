web browsers can store local data using several methods to retain information on the client side.

Let's get information How web browers store local data.


![](https://velog.velcdn.com/images/roum02/post/ee3dd147-6ca3-4267-89ee-e23993b99751/image.png)


### 1. Cookies

A cookies is small pieces of data sent from website and stored in user's web browser while the user is browsing.

1. Storage Size: Limited size is usually around 4KB per cookie.
2. Accessibility: Accessible from both client-side and server-side. it sent with **every HTTP request to the origination server.** So they can affect performace and privacy.
   they are sent to server, it is best way for server side session.

3. Expiration: They have an expiration date. or when the browser is close, they are also removed.

4. Security: As I mentioned no.3 already, They have less secure as they are sent with every HTTP request, which can expose them to network sniffing. However, they can be made more secure with the HttpOnly and Secure flags.

5. Use Case: they are often used for **session management, storing authentication token, user preferences** that need to be sent to the server.




### 2. Local Storage

A more morden way of storing data that allows for large amounts of data to be stored locally with no expiration time.

1. Storage Size: Typically the max size of storing data is 5KB per domain.

2. Accessibility: The data is not sent to the server with each request. Data is stored only in client side.

3. Expiration: the Data is persistent until explicitly deleted by JS or user.

4. Security: it is more secure than cookies but still vulnerable to XSS attacks.

5. Use Case: it used for storing large amounts of data that do not need to be sent to the server with every request, such as **user preferences, state of the application.**


### 3. Session Storage

it has smaller capacity than Local Storage, but the data is only available for the duration of the page session. it means that the data is deleted when the page session ends, like closing the tab or browser.



### Which one is more fit to store login information?


> the cookies are generally bertter suited for storing **login information **(like session token).

the reason is below.
1. Server-Side Accessibility: **Cookies allow the server to verify the user's authentication status on every request without additional effort.**
2. Security Features: Cookies can use the 'HttpOnly' flag to prevent access from JS and the 'Secure' flag to ensure access from HTTPS only
3. Session Management: Cookies are inherently designed for session management.

> Local Storage can be used for login informaion, but it has issues below.

1. Client Side only: Local storage is not accessible from the server side, so you would need to manually include authenticaton tokens in HTTP header.
2. Persistent Storage: Tockens stored in local storage is persistent until removed. it can be a security risk.
3. Security Risks: Local storage data is vulnerable to XSS attacks.

