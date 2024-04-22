# Natas 3-4 

## Description
*No description*
## Provided Information

	Username: natas4
	URL:      http://natas4.natas.labs.overthewire.org

## Solution


Upon using the credentials found in the last challenge, we can log in to the website. After logging in, we see a message that says "We are coming from an empty string, and authorized users should come only from `natas5` URL." There is also a button to refresh the page. Let's try clicking that button.


![message-without-ref](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas4-message-without-ref.png)

After clicking the button, the page refreshes, or we can say it redirects us to the `index.php` page. However, the message has changed a bit now.

![refresh-button-url-change](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas4-button-url-change.png)

Now, in the empty string, we can see the lab URL. This message means that we should visit this page from the `natas5.lab.overthewire.org` URL instead of `natas4`.

![message-with-ref](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas4-message-with-ref.png)

Checking the page source code is not helpful this time, and there is nothing we find at this point that we can use as a lead to proceed.

![page-source-code](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas4-page-source-code.png)

We can still enumerate further by analyzing the request-response. This is the part where we can learn more about the application by looking at the requests and responses. I am using Caido for this, but Burp Suite will work fine too. If you don't have an understanding of Burp Suite, don't worry. Just watch tutorials from John Hammond or Daniel Lourie.


After intercepting the request for the `index.php` page, we can see a lot of information, such as request headers, response headers, and detailed request-response flow.

![intercepted-request](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas4-request-in-caido.png)
But according to the message on the page, we know that we should visit this website from `natas5`. However, we don't have access to that URL yet. If you read about these headers, you will understand more about the application flow. In the request, we can see a header called `referrer`, which tells the server from which URL the user request is coming from.

![request-data](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas4-request.png)
If we manipulate this URL from `natas4` to the provided `natas5` URL in the request and send the request.

![refrere](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas4-ref-manipulation.png)


we can see the message "access granted" and the password for `natas5` in the response.


![response-data](/home/hackerzone/Documents/cyber_sec/github_writeups/OvertheWire_Walkthrough/Natas/natasimages/natas4-response.png)

## Conclusion
Having solid foundational skills is important. If we are doing web application testing, we should have a basic understanding of how an application works, how the request and response thing takes place, necessary request headers, how the server processes the headers, and more.

##### Happy Hacking :)
