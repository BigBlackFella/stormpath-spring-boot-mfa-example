## Stormpath Spring Boot MFA Example

This example demonstrates a flow where an multi-factor authentication (MFA) confirmation is required after each login and before gaining access to protected pages.

In particular, it uses [TOTP](https://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm) for MFA. And, it uses The [Google Authenticator](https://en.wikipedia.org/wiki/Google_Authenticator) [QR Code](https://en.wikipedia.org/wiki/QR_code) to set the shared secret. 
So, you'll want to grab a Google Authenticator compliant app for your smart phone.

TL;DR:

1. [Register](https://api.stormpath.com/register) for Stormpath
2. Save your apiKey file (Found by following the Manage API Keys link in the admin console) to: `~/.stormpath/apiKey.properties`
3. `mvn clean install`
4. `mvn spring-boot:run`
5.  Browse to: [http://localhost:8080](http://localhost:8080)

The flow looks like this:

![mfa login flow](images/MFAFlow.png)

The diagram above is not as complex as it may seem. You can think of the left and right sides as two different flows.

On the right side of the diagram, the user has not logged in yet.

On the left side of the diagram, the use has already logged in.

Both flows ensure that (a) the user sets up MFA and (b) the user has validated the latest token code after logging in, but before getting to an authenticated page.

This example takes advantage of Stormpath's [postLoginHandler](https://docs.stormpath.com/java/spring-boot-web/login.html#post-login-handler) that all of our integrations support.

Here's the typical flow:

1. Home Page - Unauthenticated

    ![home page unauth](images/HomePageUnauthenticated.png)

2. Login

    ![login](images/Login.png)

3. Create Google Authenticator MFA

    ![create ga mfa](images/CreateGAMFA.png)

4. Verify MFA Code

    ![verify ga code](images/VerifyMFACode.png)

    ![ga app](images/GAApp.png)

5. Home Page - Authenticated

    ![home page auth](images/HomePageAuthenticated.png)

6. Logout

    ![home page unauth](images/HomePageUnauthenticated.png)

7. Login

    ![login](images/Login.png)

8. Confirm Latest MFA code (No QR Code this time)

    ![confirm mfa code](images/MFAConfirmLatest.png)

9. Home Page - Authenticated

    ![home page auth](images/HomePageAuthenticated.png)