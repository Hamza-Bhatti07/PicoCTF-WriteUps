CTF: Hidden in plainsight

Description: 
 You’re given a seemingly ordinary JPG image.
 Something is tucked away out of sight inside the file.
 Your task is to discover the hidden payload and extract the flag.
 
Solution: 
 I used browser_webshell as it is always a good idea
 to download open/run unknown and malicious files with hidden
 payloads in a controlled or virtual container.
 
 By using command: wget <file-link>, the file is downloaded in webshell.
 I ran the stat command: stat img.JPG
 which gave some information about the metadata of the file.
 
 However for the detailed analysis I used https://www.metadata2go.com/
 and pasted the link of the jpg file directly there.
  
 I noticed an unusual string in the Comment field.
 
 Comment: c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9
 
 Copy pasted it into a decoder, I used: https://www.base64decode.org/
 Alternatively you could run this in the webshell: 
 echo 'c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9' | base64 --decode
 
 after decoding, the result was another hint with base64 string. 
 
 Result: "steghide:cEF6endvcmQ="
 
 Explanation: steghide, which is in their own words:
 "Steghide empowers you to conceal sensitive information 
 within everyday files like images and audio, ensuring 
 your secrets remain truly hidden in plain sight."
  
 and I found out the base64 string cEF6endvcmQ=, after decoding again, is a passkey:
 
 passkey: "pAzzword"
 
 So I looked up it's commands, and found this: 
 steghide extract -sf "filename.jpg" -p "passkey"

 So I ran the following in the webshell:
 steghide extract -sf "img.jpg" -p "pAzzword" 
 and got the flag.
 
 
 
 