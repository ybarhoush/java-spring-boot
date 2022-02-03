# java-spring-boot
Spring Project Layout and Running Locally
follows the tutorial
https://github.com/spring-guides/tut-spring-boot-oauth2/tree/main/simple

== What Just Happened?

The app you just wrote, in OAuth 2.0 terms, is a _Client Application_, and it uses the https://tools.ietf.org/html/rfc6749#section-4[authorization code grant] to obtain an access token from GitHub (the Authorization Server).

It then uses the access token to ask GitHub for some personal details (only what you permitted it to do), including your login ID and your name.
In this phase, GitHub is acting as a Resource Server, decoding the token that you send and checking if it gives the app permission to access the user's details.
If that process is successful, the app inserts the user details into the Spring Security context so that you are authenticated.

If you look in the browser tools (F12 on Chrome or Firefox) and follow the network traffic for all the hops, you will see the redirects back and forth with GitHub, and finally you'll land back on the home page with a new `Set-Cookie` header.
This cookie (`JSESSIONID` by default) is a token for your authentication details for Spring (or any servlet-based) applications.

So we have a secure application, in the sense that to see any content a user has to authenticate with an external provider (GitHub).

We wouldn't want to use that for an internet banking website.
But for basic identification purposes, and to segregate content between different users of your site, it's an excellent starting point.
That's why this kind of authentication is very popular these days.

In the next section, we are going to add some basic features to the application.
We'll also make it a bit more obvious to users what is going on when they get that initial redirect to GitHub.