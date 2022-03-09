# Remote Desktop Protocol (RDP)

## **Scenario**

> An interplanetary illegal dealer was using a remote machine to store all his Trade secrets. Intelligence team of the solar system identified that the dealer was from Earth. When investigated, it was found that the dealer was maintaining a clean machine in his home and storing all his trade secrets in a remote machine via RDP. Unfortunately, the remote machine was destroyed. The only source of evidence we have is the forensic disk image of the clean machine. Show your forensic skills. Help the investigators in cracking the trade secrets like the dealer’s crypto wallet address, his customer details etc. Note: This is a work of fiction. Names, characters, places and incidents either are products of the author's imagination or are used fictitiously.

### Questions

> Question 1) Submit the USERNAME of the dealer's machine from which the forensic disk image was created (Format: username)_(2 points)_
>
> _💡_ **Answer:** `spiderman`

To begin this question, I initiated the machine. Upon logging in, I glanced around the desktop icons looking for what I was going to look at first, since i'm not well versed in digital forensics i'm trying to improvise. I first opened up the Evidence folder and saw there was a text file named `RDPCache.ad1` since this lab is about an actor storing all his trade secrets in a remote machine via RDP, this appeared interesting to me.&#x20;

The text file was created by AccessData FTK imager, AccessData FTK is a computer forensics software, it scans a hard drive looking for various information. An example of what it can locate is deleted emails, it can also scan a disk for text strings to sue them as a password dictionary to crack encryption.

From looking at the text file, it seems the source disk for the information captured by the FTK comes from `C:\Users\`**`spiderman`**`\Desktop`

This tells me this is the username of the dealer's machine.

![](<../.gitbook/assets/Untitled 2.png>)

