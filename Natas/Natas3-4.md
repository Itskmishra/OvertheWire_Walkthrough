# Natas 3-4 

## Description
*No description*
## Provided Information

	Username: natas4
	URL:      http://natas4.natas.labs.overthewire.org

## Solution


Upon using the credentials found in the last challenge, we can log in to the website. After logging in, we see a message that says "We are coming from an empty string, and authorized users should come only from `natas5` URL." There is also a button to refresh the page. Let's try clicking that button.








![natas4-message-without-ref](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/31e826a0-a194-497a-b29a-baefa4e2a286)

After clicking the button, the page refreshes, or we can say it redirects us to the `index.php` page. However, the message has changed a bit now.

![natas4-button-url-change](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/60750109-f791-4bb3-897e-bf0a770ab2cf)

Now, in the empty string, we can see the lab URL. This message means that we should visit this page from the `natas5.lab.overthewire.org` URL instead of `natas4`.

![natas4-message-with-ref](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/f856888b-47ea-41f7-a56c-2b01cf2475d2)

Checking the page source code is not helpful this time, and there is nothing we find at this point that we can use as a lead to proceed.

![natas4-page-source-code](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/22b9e846-6cf2-4ea2-ab6a-c63987292a18)

We can still enumerate further by analyzing the request-response. This is the part where we can learn more about the application by looking at the requests and responses. I am using Caido for this, but Burp Suite will work fine too. If you don't have an understanding of Burp Suite, don't worry. Just watch tutorials from John Hammond or Daniel Lourie.


After intercepting the request for the `index.php` page, we can see a lot of information, such as request headers, response headers, and detailed request-response flow.

![natas4-request-in-caido](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/0ec81ce0-23a8-441d-9baa-b9eb62139cfb)

But according to the message on the page, we know that we should visit this website from `natas5`. However, we don't have access to that URL yet. If you read about these headers, you will understand more about the application flow. In the request, we can see a header called `referrer`, which tells the server from which URL the user request is coming from.

![natas4-request](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/c8151ef5-8da2-46b5-a08f-2088700e0720)
If we manipulate this URL from `natas4` to the provided `natas5` URL in the request and send the request.

![natas4-ref-manipulation](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/29503c91-a77a-4b25-ba31-c413efec9287)

we can see the message "access granted" and the password for `natas5` in the response.

![natas4-response](https://github.com/Itskmishra/OvertheWire_Walkthrough/assets/141756495/ece74b16-3c9a-4d8c-837d-51fa1ac15cc2)

## Conclusion
Having solid foundational skills is important. If we are doing web application testing, we should have a basic understanding of how an application works, how the request and response thing takes place, necessary request headers, how the server processes the headers, and more.

###### Happy Hacking :)
