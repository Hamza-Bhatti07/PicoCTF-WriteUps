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
 <img width="919" height="357" alt="image" src="https://github.com/user-attachments/assets/bf592d3d-0b8f-4045-a178-1ada0703a815" />
  
 I noticed an unusual string in the Comment field.
 
 Comment: c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9
 
 Copy pasted it into a decoder, I used: https://www.base64decode.org/
<img width="844" height="672" alt="image" src="https://github.com/user-attachments/assets/ddbc4ec3-70e7-44dc-bbb5-567106e912a7" />

 
 Alternatively you could run this in the webshell: 
 echo 'c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9' | base64 --decode
 
 after decoding, the result was another hint with base64 string. 
 
 Result: "steghide:cEF6endvcmQ="
 
 Explanation: steghide, which is in their own words:
 "Steghide empowers you to conceal sensitive information 
 within everyday files like images and audio, ensuring 
 your secrets remain truly hidden in plain sight."
  
 and I found out the base64 string cEF6endvcmQ=, after decoding again, is a passkey:
 <img width="848" height="664" alt="image" src="https://github.com/user-attachments/assets/abf67f02-0043-4538-b1a2-15811ba03e9a" />

 passkey: "pAzzword"
 
 So I looked up it's commands, and found this: 
 steghide extract -sf "filename.jpg" -p "passkey"

 So I ran the following in the webshell:
 steghide extract -sf "img.jpg" -p "pAzzword" 
 and steghide wrote the extracted data to flag.txt
 <img width="630" height="79" alt="image" src="https://github.com/user-attachments/assets/faf0721c-7181-4b52-aa13-8c4e4470db42" />

That's all folks. Thank you for reading.


 
 
 

 
