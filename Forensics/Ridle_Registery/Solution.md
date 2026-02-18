picoCTF: Riddle Registry <?>
Category: Forensics

Description: 
 You've stumbled upon a peculiar PDF filled with what seems like nothing
 more than garbled nonsense. But beware! Not everything is as it appears.
 Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered.
 "uncover the flag within the metadata."

Solution:
 Download the file via the given link if you want to solve locally.
 Or use the browser_web_shell and wget command: wget <file-path>.
 
 The description clearly suggests that you will find nothing inside the file.
 so ignore the contents of the file and go straight to file properties.
 I however went through the file as it too had it's own challenges
 which were "misleading" but interesting regardless.
 
 You can also use online tools for viewing detailed metadata,
 I used https://www.metadata2go.com/.
 you'll find that all text seems readable and normal
 except the author name which is a string with an equals to (=) sign at the end.
 
 author: cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV8zNTc4NzM5YX0=
 
 This is very unusual for a username, so I copied it and looked it up.
 It is a Base64 string! But we normally use UTF-8.
 UTF-8 is a character encoding standard used for electronic communication.
 Defined by the Unicode Standard,the name is derived from 
 Unicode Transformation Format – 8-bit. And as of 2026,
 almost every webpage (99%) is transmitted as UTF-8.
 
 So I looked up for a decoder, and found https://www.base64decode.org/.
 Pasted the string and voilà. I found the now decoded flag.

Credits:
Thanks to @Cyber-Connect-pk https://github.com/Cyber-Connect-pk for
hosting weekly CTFs like these to help us improve our CTF solving skills!

