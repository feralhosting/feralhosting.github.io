
Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot.

Use this link in your Account Manager to access the relevant slot:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)

You login information for the relevant slot will be shown here:

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)

Filezilla
---

This is a basic guide on connecting to your Feral slot using FTP/SFTP with FileZilla.

Please download and install Filezilla if you have not already done so.

[Filezilla Client Download Page / Multi platform](https://filezilla-project.org/download.php?type=client)

Once you have installed Filezilla, run the application and you will be able to work through the images.

The Layout explained:
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/1.png)

Accessing the Site Manager:
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/2.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/3.png)

The Site Manager: Adding a New Site:
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/5.png)

Naming your new connection profile:
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/6.png)

If you wish to connect using unencrypted FTP use this image below or skip this image:
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/7.png)

If you wish to use encrypted SFTP to connect use this information scheme:
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/8.png)

Connecting to your slot using this profile:
---

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/9.png)

**Important note:** After clicking Connect or OK this site will now be saved to the Site Manager for future use or using quick connects as shown in image 3.

You have now completed the basic steps for creating a profiles and connecting to your slot using Filezilla. You can stop here.

Optional Step - Using a public/private key pair:
---

**Important note:** This step is OPTIONAL and does not need to be completed to access your slot.

If you need to use a keyfile for connecting please follow the steps in these images below for adding your key to Filezilla according to these rules:

**1:** Your keyfile must be in the Putty tools `.PPK` format on Windows. See this guide for keyfile creation:

[Setting up Public Key Authentication for Password-less Login](https://www.feralhosting.com/faq/view?question=13)

**2:** Filezilla does not directly support passphrase protected keyfiles, PAGEANT must be used in windows to load the passphrase into memory. See this guide: [PAGEANT](https://www.feralhosting.com/faq/view?question=241)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/10.png)

![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/SFTP%20and%20FTP/FTP%20and%20SFTP%20basics%20-%20Filezilla/11.png)



