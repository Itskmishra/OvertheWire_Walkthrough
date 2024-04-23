# Natas 4-5

## Description
*No description*
## Provided Information
	Username: natas5
	URL:      http://natas5.natas.labs.overthewire.org
 
## Solution

Upon logging in, we encountered a message that read, "access disallowed. You are not logged in." However, as we had just entered our login credentials, it became apparent that the message was not referring to our login status. There was no information available on the page or in the source code, so we decided to analyze the request.

![natas5-login-message](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/1b3dca03-da83-4146-b618-b409a7851388)

We utilized tools such as Caido, BurpSuite, and ZAP to intercept the request and examine it. 

![natas5-intercepted-request-response](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/954e4ade-4adc-4199-b7b4-41c1a7a55b01)

By analyzing the request format, we discovered that it was passing cookies with three different values. The first two were not useful, but the third value was `loggedin=0`. In computer language, `0` means false, and `1` means true. Therefore, `loggedin=false`. We changed this value to `1`, which meant `loggedin=true`. 

![natas5-req-analysis](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/a5b2e1ed-d390-42da-9b10-ebbdfc2319aa)

Send the request to the repeater in BurpSuite and replayed it in Caido. 

![natas5-request-manipulation](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/08a35830-a8d0-43b9-af67-aab48b10a1ff)

We then sent the modified request with the updated cookie value. As a result, we were granted access, and the password for natas6 was returned. 

![natas5-response](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/07d9298e-cefb-4bf9-ad9d-8e4513047a04)


## Conclusion
It is important to understand all basic headers in the context of web application testing. Ethical hackers must try out different approaches to achieve their goals.

###### Happy Hacking :)
