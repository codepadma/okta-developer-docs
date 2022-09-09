---
title: Sign in with email only
---

<ApiLifecycle access="ie" /><br>

Enable users to sign in with email only in an application using the embedded Okta Sign-In Widget.

**Learning outcomes**

* Configure your Okta org to enable user sign-in without a password.
* Integrate password-optional sign-ins in your app using the Sign-In Widget

**What you need**

<StackSnippet snippet="whatyouneed" />
</br>

**Sample code**

<StackSnippet snippet="samplecode" />

---

## Update configurations

<StackSnippet snippet="setupoktaorg" inline/>

> **Note:** To test the sign-in integration, you must use a user with an enrolled email authenticator.

## Integrate into your app

### Summary of steps

The following diagram details the steps involved in an email-only sign-in flow.

<StackSnippet snippet="integrationsummary" />

### 1. The user submits their username

The user enters their username and clicks the **Next** button to start the sign-in flow.

> **Note:** This guide assumes you have already set up and configured the Sign-In Widget. To learn how to add the Sign-In Widget to your app, see [Embedded Okta Sign-In Widget fundamentals](docs/guides/embedded-siw/main/).

<div class="half">

![Screenshot showing the Sign-in Wiget sign-in page with a username field and a Next button.](/img/pwd-optional/pwd-optional-widget-sign-in-page.png)

</div>

### 2. The user starts the email challenge flow

The Sign-In Widget displays a page for the user to start verifying their identity by email. Email is the only choice because:

* The user has only enrolled the email authenticator.
* Email is the only allowed authentication factor in your app integration's authentication policy.

The user clicks **Send me an email** to begin the email challenge flow.

<div class="half">

![Screenshot showing the Sign-in Wiget verify-email page with a Send me an email button.](/img/pwd-optional/pwd-optional-widget-send-email-page.png)

</div>

### 3. The user verifies their identity with the email authenticator

Identity Engine sends a verification email to the user's primary email address. The email gives the user two ways to verify their identity:

* Copy a One-Time Password (OTP) from the email into the Sign-In Widget and submit it for verification.
* Click a "magic link" in the email that submits the OTP to Identity Engine on your behalf.

Your app requires no changes to use OTP since it's built into the Sign-In Widget. However, using magic links require additions to your app which include:

* A check to ensure the user starts the sign-in flow and opens the magic link in the same browser.
* And endpoint to handle the callback request originating from the magic link. This method takes the values from the `otp` and `state` query parameters in the request and passes them to the Sign-In Widget.

>**Note**: For more information on magic links and OTP, including customizations and complete user journeys, see the [Email Magic Links Overview](docs/guides/email-magic-links-overview/main/).

<StackSnippet snippet="integrationsteps" />