Welcome to PBP - Pretty Bad Privacy!
=====================


Summary
---------

This is a small script that allows you to permanently decrypt PGP encrypted mails you have received in Apple Mail. Why would you want to do so? Because only if you permanently decrypt your mail, it will be searchable through Apple's Spotlight index. Why would you <i>not</i> want to do so? Same reason. In other words, this script only makes sense for you to use if your using PGP for that particular mail is really designed as a transport encryption, not as an encryption at rest (on your disk).

Which is quite regularly the case for me, which is why I wrote that script: If I can't take care of my own disk then I've some other problems to worry about. Plus, it is up to you on which mail you really want to use it. 

If you use this process, your previously Pretty Good Privacy for that mail will become Pretty Bad Privacy - hence the name of this script.

Installation
---------

Copy the pbp file into some directory that is in your path. Also, make sure you have the following bits installed: 

1. Perl with MIME::Base64: You should have that anyway.
2. GPG Tools (<http://gpgtools.org>): Otherwise you would probably not be using this script in the first place...
3. Mac Ports (<http://macports.org>): Because of the following:
4. MPack: To extract the attachment. Install it using:

```
# sudo port install mpack
```

Usage
---------

So as you receive a mail that you want to permanently decrypt, do the following process:

* Drag and drop that mail to some folder, e.g., your desktop. It'll automatically have some name with the subject line, and a file extension .eml. Let's assume the file is named xyz.eml.
* Open a Terminal window and change to the directory you just dragged that mail to:

```
# cd ~/Desktop
```

* Execute the following command:


```
# pbp xyz.eml
```

* This will create a file decrypted.eml. Notice that it will temporarily also create a file encrypted.asc. Notice also that both files are going to be overwriting files of the same name, should they already be there. Feel free to add any better checking to the code should you so desire. Hey, the program's name starts with 
"Pretty Bad", so what do you expect anyway.

* Now since you have this new decrypted.eml file, you can close your terminal window and double click that file. It should be opened in Apple Mail.

* From there, you  just choose, from the menu, "Email" and then  "Move To..." - and you then select as target folder exactly the location out of which you had dragged the mail onto your desktop in the first place. Since the decrypted mail maintains exactly the same header structure, i.e., among other things, also the message ID, from the original mail, moving the decrypted mail into the same place will effectively replace the encrypted mail by the decrypted one.

* As final cleanup, you can remove the both the decrypted and the encrypted mails from the folder you were working in (e.g., your Desktop).


Optimizations
---------

Many things can be done to make this script better:

1. For example, it has many things hard coded, for example, not only the file names,
2. but also the header strings by which it finds out at which point it wants to stop collecting headers (status 1), at which point it has found the beginning of the attachment that contains the encrypted part of the mail (status 2), at which that attachment's content actually starts (status 3) and ends (status 4).
3. Also, you could think about embedding this into Apple Mail by some scripting foo. But then it would probably be best to actually just include the same logic into GPGMail in the first place. As you can read elsewhere, this has been one of the first requirements on the GPGMail list, but apparently has never been implemented.

