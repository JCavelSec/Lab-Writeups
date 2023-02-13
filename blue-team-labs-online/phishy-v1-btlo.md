# 📝 Phishy V1 BTLO

### **Scenario** <a href="#969c9a08-be6b-49c2-8592-b58076e9b0d5" id="969c9a08-be6b-49c2-8592-b58076e9b0d5"></a>

> You have been sent a phishing link - It is your task to investigate this website and find out everything you can about the site, the actor responsible, and perform threat intelligence work on the operator(s) of the phishing site.

💡Warning: The website and kit you see in the lab are REAL. Exercise caution when interacting with the malicious website and do not enter any sensitive information

### Questions <a href="#8bdb9234-725b-4353-a7aa-d8bc7d28521f" id="8bdb9234-725b-4353-a7aa-d8bc7d28521f"></a>

> 1\. The HTML page used on securedocument.net is a decoy. Where was this webpage mirrored from, and what tool was used? (Use the first part of the tool name only)_(4 points)_

💡**Answer**: `61.221.12.26/cgi-sys/defaultwebpage.cgi, HTTrack`

To figure this part out, we navigated to securedocument.net/secure. This part was a little confusing for me and I had to use a write-up because I wasn’t sure how to get here, if I had access to DirBuster, it would’ve been the first tool I would’ve used in order to bruteforce and find directories.

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_4.55 (1) (1).57\_PM>)



We can see that from here, the Parent Directory is available, the Phishing kit is also here, `0ff1cePh1sh.zip`, we will be using this later.

Clicking on Parent Directory redirected us to `http://securedocument.net/cgi-sys/`

We viewed the page source and found where this webpage was mirrored from as well as what tool was used.

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_5.01 (1).45\_PM>)



Here we can see it is mirrored from `61.221.12.26/cgi-sys/defaultwebpage.cgi`

The tool used is `HTTrack Website Copier`

> 2\. What is the full URL of the background image which is on the phishing landing page?_(3 points)_

💡Answer: [`http://Securedocument.net/secure/L0GIN/protected/login/portal/axCBhIt.png`](http://securedocument.net/secure/L0GIN/protected/login/portal/axCBhIt.png)``

To find the URL of the background image, all we have to do is right click the image itself, behind the login form and inspect element, from there navigate to “Style Editor”, I first thought we could find the URL by just using inspect element on the image itself, but that didn’t work, I looked around the page source and the image couldn’t be found anywhere. My next step was to check CSS. From there, we found the styling sheet `style.css` , the first rule we can see is the body rule.

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_5.12 (2).02\_PM>)



From this rule, we can see what url is used for the background, `axCBhIt.png`

If we add this to the URL, `http://securedocument.net/secure/L0GIN/protected/login/portal/axCBhIt.png`

We are redirected to the image itself, I first got the answer wrong because I didn’t realize the 0 in `L0GIN`, so don’t make the same mistake I did!

> 3\. What is the name of the php page which will process the stolen credentials?_(3 points)_

💡**Answer: `jeff.php`**

The way we figure this out is by looking at the page source again, we can see that the login form has a form action,

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_5.19 (2).25\_PM>)



We can see it here, `<form action=”jeff.php” method=”post”>`

This uses a HTTP POST request method.

> The HTTP POST method requests the web server accept the data enclosed in the body of the POST message. HTTP POST method is often used when submitting login or contact forms or uploading files and images to the server.

When the victim clicks the download button, the POST method will be used, this also executes the form action, jeff.php, which will process the credentials entered in the login form.

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_5.25 (1).44\_PM>)

This is the PHP script, Jeff.php

> 4\. What is the SHA256 of the phishing kit in ZIP format? (Provide the last 6 characters)_(3 points)_

💡**Answer:** `fa5b48F`

For this question we will be using the file we found earlier, `0ff1cePh1sh.zip`

To get the SHA256 hash of the phishing kit we will be using the sha256sum linux command,

sha256sum:

> Print or check SHA256 (256-bit) checksums. With no FILE, or when FILE is -, read standard input.

💡[`https://linux.die.net/man/1/sha256sum`](https://linux.die.net/man/1/sha256sum)``

To use this command, launch the terminal, and cd (Change Directory) to the directory where you downloaded the Phishing kit.

In my case, the default downloads folder is `/home/ubuntu/Downloads`

Enter these two commands in to the terminal, one by one.

> cd /home/ubuntu/Downloads

> sha256sum 0ff1cePh1sh.zip

The terminal responds with the SHA256 hash of the zip file.

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_5.39 (2).41\_PM>)

An alternative to using cd to navigate directories is going to the directory yourself using the file manager and right clicking the directory and clicking `“Open Terminal Here”`

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_5.36 (1) (1).11\_PM>)

> 5\. What email address is setup to receive the phishing credential logs?_(3 points)_
>
> _💡_**Answer:** `boris.smets@tfl-uk.co`
>
> This can be found by looking at the PHP script from earlier (jeff.php).&#x20;

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_5.25 (2).44\_PM>)

Here we can see the recipient, this script has this email setup to receive the phishing credential logs. You can find it under "recipient".

> 6\. What is the function called to produce the PHP variable which appears in the index1.html URL?
>
> **💡Answer:** `getTime()`

Open the `index.html` file, you will notice a javascript function `(getTime)` is ran which produces the timestamph in PHP.

![](<../.gitbook/assets/Screen Shot 2022-03-07 at 7.04.25 PM.png>)

> What is the domain of the website which should appear once credentials are entered?_(3 points)_
>
> 💡**Answer:** `Office.com`

![](<../.gitbook/assets/Screen\_Shot\_2022 03 07\_at\_5.25 (2).44\_PM>)

Here we can see that the script that runs after the login form is submitted is at the end of the script, `https://www.office.com` will be the result.

> 7\. There is an error in this phishing kit. What variable name is wrong causing the phishing site to break? (Enter any of 4 potential answers)_(3 points)_
>
> _💡_**Answer:** `userrr`

![](<../.gitbook/assets/Screen Shot 2022-03-07 at 7.12.53 PM.png>)

This can be found by looking at the page source, this causes the phishing site to break. There are apparently 3 other potential answers but this was the first one i spotted, as well as `passss` being used instead of `pass`

__
