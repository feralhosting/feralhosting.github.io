### Background

FTP and SFTP are good ways to transfer data between a seedbox and a personal computer, but there is a problem: Many FTP/SFTP clients use "ASCII mode" to transfer .CUE, .LOG, and .M3U files, and this can modify the files and cause hash check failures. That can cost you precious ratio, if you don't notice it in time.

### Why this happens

FTP can transfer files in either of two "modes":

— binary mode transfers an exact copy, byte for byte.

— ASCII mode modifies the file. Most often, this means that the way a new line is encoded is changed. On Windows PCs, new lines are demarcated by the bytes \x0D\x0A. On Mac OS X and Linux, new lines are demarcated by \x0A. You might think, "this won't be a problem for me, I use the same operating system on my seedbox and my laptop," but it is still a problem because you may not be using the same operating system as the person who created the torrent. If Alice creates a torrent on a PC which includes \x0D\x0A, and then Bob downloads it onto his Mac seedbox, the download will still be PC-formatted. He can seed it without hash check failures. If Bob then FTPs this file over to his other Mac using "ASCII mode", it will "translate" that \x0D\x0A into \x0A. If Bob then tries to seed it, there will be a hash check failure because the file has changed.

### How to fix it

Set your FTP client to ALWAYS use binary mode. Note: This is not possible in some FTP clients. In that case, you need to find a different FTP client.

**Specific advice for Mac users:**

1. Install Fetch.

2. Go to the Fetch menu and select "Preferences", then go to the "Download" tab.

3. Set "Default download mode" to "Binary".

4. Uncheck the box for "Decoding and expansion" — leaving this box checked can lead to hash check failures, because it will unzip .ZIP files, etc.

5. Go to the "Upload" tab, and set "Default upload format" to "Binary (raw data)".

6. Go to the "Obscure" tab, and under "Editing text files" uncheck the box for "Use text mode transfers". For some stupid reason, this actually matters even if you aren't editing text files. This may be a bug.

7. Quit Fetch and then restart.

---
The guide was originally [posted on what.cd](https://ssl.what.cd/forums.php?action=viewthread&threadid=99575) by user bollweevil.