---
layout: post
title: Paperify - Backup your files on paper using QR Code
---

Paperify: How to backup data using QR-Code and print them on paper?

[Read on Medium](https://medium.com/@alisina.bm/paperify-how-to-backup-data-using-qr-code-and-print-them-36d12eaed8fe)

If you’re they type of person who always thinks about apocalyptic destruction like I am, One of the things that scares me a lot is loosing all my digital data. Private Keys, Password Manager data, Cryptocurrency wallet seeds/private keys. These are all things that I prefer not to store anywhere on the else than my own computer.

> **TL;DR:**  
> You can use [github.com/alisinabh/paperify](https://github.com/alisinabh/paperify) to convert your files to multi page QR Codes, print them and then restore them whenever you want to.

I know it may sound crazy but lets say there were a powerful EMP Gun (Electro Magnetic Pulse) has gone off in your neighborhood and all your data on your SSD, USB Disks and other means of digital storage is lost. What can you do to prevent it?

One thing that came to my mind was using what Github did with its [Arctic Code Vault](https://archiveprogram.github.com/) program. They stored binary binary data using 2D-barcodes on film. I really liked this idea because there are no mechanical or electrical components used in it and if you keep them in good environment they will last for a really long time. So why not use the same approach to store our important data using printers?

So I’ve got excited and first thing that came to my mind was using [qrencode](https://fukuchi.org/works/qrencode/) which is a simple command line tool for creating QR-Codes. At first, It looked so simple. Just run “$> _qrencode -r yourfile.ext -o image.png”_ and you will get the QR-Code for your file,right?

Well, Not so simple! First of all normal QR codes do not support binary data. But that can be an easy fix, Just encode them in base64 and then pass them to qrencode. But again **not so simple**. You see, using base64 actually will make your data bigger and it’s not efficient but keeping that aside, QR codes have their own limitations. One of them is how much data they can handle. According to qrencodes man page, The largest supported QR code is 177x177 modules long. Without any error corrections (which is dangerous) this will give us roughly 4000 characters to work with (Which will be 3000 bytes). So what can we do to backup our files which are larger than 3KB?

One simple solutions is just slicing our file to 3KB chunks, Then using qrencode on each chunk to make a QR-Code of that chunk and then when we want to restore our files, we can just glue these chunks back together in one file. So I decided to create a script for this. It’s called [**paperify**](https://github.com/alisinabh/paperify).

### How to use paperify?

paperify_.sh_ works in these stages.

 1. Uses “_split”_ to split your file into chunks of 2953 bytes.
 2. Uses “_qrencode_” to convert each chunk to a QR-code image respectively.
 3. Uses “_imagemagick_” to add human readable metadata to the generated codes. and make them printable on A4 papers.

First make sure you have qrencode and imagemagick installed.  
Then you can simply clone paperify and run:

```
$> ./paperify.sh my\_secret\_files.tgz  
processing my\_secret\_file.tgz-000  
processing my\_secret\_file.tgz-001  
processing my\_secret\_file.tgz-002  
processing my\_secret\_file.tgz-003  
processing my\_secret\_file.tgz-004QR Code generation completed  
You can now print files inside of my\_secret\_file.tgz-qr
```

Wallah! 😱 You have created print ready codes of your file. Make sure to store them somewhere safe.

Currently the generated codes use 8-bit mode which means they store binary data directly on the QR codes.

### How to restore my data from these codes?

Just scan your documents using a scanner (recommended) or a mobile phone camera. Then put all the images inside a folder.  
**IMPORTANT**: Please make sure your scanned files are in the correct order! I recommend scanning them in the correct order so you don’t need to rename the files. And don’t put anything else in your scanned image directory.

Just make sure you have “Zbar” installed on your system.  
Again you can clone paperify and simply run:

```
$> ./digitallify.sh my\_secret\_restored\_files.tgz scanned\_images\_dir  
reconstructing my\_secret\_file.tgz-000.png  
reconstructing my\_secret\_file.tgz-001.png  
reconstructing my\_secret\_file.tgz-002.png  
reconstructing my\_secret\_file.tgz-003.png  
reconstructing my\_secret\_file.tgz-004.pngFile reconstructed as my\_secret\_restored\_files.tgz please check the bellow sha1 with the sha1 of the file in your media.  
**53b37589f2d7363010fc4aa8bb85d4e8c5f3741a**  my\_secret\_restored\_files.tgz
```

And you will have your file reconstructed as _my\_secret\_restored\_files.tgz_. There is one more extra step to verify that the printed sha1 (**53b37589f2d7363010fc4aa8bb85d4e8c5f3741a**)  with the sha1 in one of your printed files named **FINAL SHA1**.


If they both matched, Congrats 😃 You have your file restored!

If they did not match, there are two probabilities.

1.  The order of your scanned files are incorrect. Check the file names with the printed **CHUNK** number in your images.
2.  One of the images has bad quality, Try re-scanning them all. Please use a decent scanner with 300dpi resolution.

### Storage

As of today, Each page created with paperify can hold up-to 2953 bytes of data. So for example a 100KB file will take 35 pages, a 1MB file would take 356 pages. So for files larger than 290KB (~100 pages) it would **not** be convenient to use paperify.

Please store your data somewhere safe! Remember that you are responsible for your data. If you want to store something confidential please consider encrypting it first with tools like gpg.

Thank you for your time. If you liked it, Please give it a star on Github.  
[github.com/alisinabh/paperify](https://github.com/alisinabh/paperify)

Have Fun!
