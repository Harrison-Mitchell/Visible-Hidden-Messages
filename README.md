# Visible Hidden Messages
Hide data invisibly. Uses zero width unicode characters to format data into binary which piggyback's onto a visible message.

### Live demo
Found [here](harrisonm.com/vhm.html).

### How it works
Unicode has lots of characters for visual communication. English characters as seen here, Chinese characters, emojis, playing cards... There are also semantic only characters such as the right to left character used in cases such as displaying Arabic which reads from the right. Two of these semantic characters are the "Zero width space" which is used to signify a good place to split text to a new line. E.g pop<ZWS>ulation. A new line will be placed there with a dash to continue the word over the line. Another character is the "Zero width joiner" which does the reverse. I use these characters for the fact that they're zero width, i.e invisible. U+200B and U+200D are then used to represent binary (0 and 1) to store data.
  
### Uses
Nothing practicle, but that's the point of a demo. I've thought of two use cases so far:
* Display sensitive infomation with the user's IP address encoded in the message so if they were to copy and paste the information and leak it, they can be traced back.
* The Australian government forces you to implement a backdoor and you message your boss: "I love the Australian government!" and encoded in the message is "I'm under duress, please save me"

### Encoding files - Advanced
Uses common UNIX utilities to convert files to hex and back again.
* Do a hexdump of your file, remove new lines and copy it to the clipboard:
* `xxd -p inFile | tr -d '\n' | xclip -selection c`
* Encode it, send.
* Recieve, decode, copy message to clipboard.
* Use the data from your clipboard to reassemble the file:
* `xclip -selection c -o | xxd -r -p > outFile`

### Limitations
* Some platforms may trim the data
* Messages that are too long may cause you to go over the max message length of some platforms
