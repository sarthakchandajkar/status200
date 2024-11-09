---
title: SSPR
aliases:
  - SSPR
draft: false
tags:
  - AZ-104
  - Cloud
  - Microsoft
author:
  - Sarthak Chandajkar
---
- reset forgotten password in web browser
- reduces the load on administrators
- minimizes the productivity impact of a forgotten or expired password
- can be deployed with password writeback using [[Microsoft Entra Connect]] or cloud sync.

## Working of SSPR

After the *Forgot Password* prompt:
1. Localization
2. Verification
3. Authentication
4. Password reset
5. Notification

## Authentication Methods

|Authentication method|How to register|How to authenticate for a password reset|
|---|---|---|
|Mobile app notification|Install the Microsoft Authenticator app on your mobile device, then register it on the multifactor authentication setup page.|Azure sends a notification to the app, which you can either verify or deny.|
|Mobile app code|This method also uses the Authenticator app, and you install and register it in the same way.|Enter the code from the app.|
|Email|Provide an email address that's external to Azure and Microsoft 365.|Azure sends a code to the address, which you enter in the reset wizard.|
|Mobile phone|Provide a mobile phone number.|Azure sends a code to the phone in an SMS message, which you enter in the reset wizard. You can also choose to get an automated call.|
|Office phone|Provide a nonmobile phone number.|You receive an automated call to this number and press #.|
|Security questions|Select questions such as "In what city was your mother born?" and save their responses.|Answer the questions.|

## Recommendations

- Enable two or more of the authentication reset request methods.
- Use the mobile app notification or code as the primary method. But also enable the email or office phone methods to support users without mobile devices.
- The mobile phone method isn't a recommended method, because it's possible to send fraudulent SMS messages.
- The security-question option is the least recommended method, because the answers to the security questions might be known to other people. Only use the security-question method in combination with at least one other method.


> [!NOTE] Administrator Role
> The security-question method isn't available to accounts associated with an administrator role


> [!WARNING] Hybrid Situation
> In a hybrid situation, where you have Active Directory on-premises and Microsoft Entra ID in the cloud, any password change in the cloud must be written back to the on-premises directory. This writeback support is available in Microsoft Entra ID P1 or P2. It's also available with Microsoft 365 Apps for business.


## Scope

- None(Default)
- Selected
- All

