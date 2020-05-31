---
description: Windows Guides and How-To, examples and simple usage
---

# Windows Guides and How-To

## Auto Login Without Password at Boot

Hit WIN+R or from start menu search `run` and press enter.  
At run dialog enter `netplwiz`:

![run dialog](../assets/images/windows/2018-10-21_09-24-24_runNetplwiz.png "run dialog")

* In the User Accounts dialog box, click the account you want to automatically log on to.If it is available, clear the Users Must Enter A User Name And Password To Use This Computer check box.
* Click OK.
* In the Automatically Log On dialog box, enter the user’s password twice and click OK.

![usersAccounts](../assets/images/windows/2018-10-21_09-23-36_usersAccounts.png "usersAccounts")

The next time you restart the computer, it will automatically log on with the local user account you selected. Configuring automatic logon stores the user’s password in the registry unencrypted, where someone might be able to retrieve it.

## Add Program to Startup - Windows 7,8,10 & Servers

Hit WIN+R or from start menu search `run` and press enter.  
At run dialog enter `shell:common startup`:

![shell:common startup](../assets/images/windows/2018-10-21_09-52-21_runStartup.png "shell:common startup")

* Create shortcut for the program you want to auto startup when Windows boots.
* Move the shortcut to the `Startup` folder that opened before.

## Reboot or Shutdown Windows From Command Line (CMD)

Reboot windows computer
This command will set a time out of 10 seconds to close the applications. After 10 seconds, windows reboot will start.

```cmd
shutdown /r /t 10
```

Force reboot

```cmd
shutdown /r /f /t 0
```

Force Shutdown

```cmd
shutdown /s /f /t 0
```

## Send Emails From The Windows Task Scheduler

First, [download SendEmail](https://github.com/fire1ce/sendEmail-windwos-v1.56/archive/master.zip "SendEmail"), a free (and open source) tool for sending emails from the command line. Extract the downloaded archive into a folder on your computer.

![SendEmails](../assets/images/windows/sendMail/sendMail1.png)

Next, launch the Windows Task Scheduler and create a new task – consult our guide to creating scheduled tasks for more information. You can create a task that automatically sends an email at a specific time or a task that sends an email in response to a specific event.

When you reach the Action window, select Start a program instead of Send an e-mail.

![SendEmails](../assets/images/windows/sendMail/sendMail2.png)

In the Program/script box, use the Browse button and navigate to the SendEmail.exe file on your computer.

![SendEmails](../assets/images/windows/sendMail/sendMail3.png)

Finally, you’ll have to add the arguments required to authenticate with your SMTP server and construct your email. Here’s a list of the options you can use with SendEmail:

### Server Options

> * -f EMAIL – The email address you’re sending from.  
> * -s SERVER:PORT – The SMTP server and port it requires.  
> * -xu USERNAME – The username you need to authenticate with the SMTP server.  
> * -xp PASSWORD – The password you need to authenticate with the SMTP server.  
> * -o tls=yes – Enables TLS encryption. May be necessary for some SMTP servers.  

__If you’re using Gmail’s SMTP servers, these are the server options you’ll need:__

> * -s smtp.gmail.com:587 -xu you@gmail.com -xp password -o tls=yes

Of course, you’ll have to enter your own email address and password here.

### Destination Options

> * -t EMAIL – The destination email address. You can send an email to multiple addresses by including a space between each address after the -t option.  
> * -cc EMAIL – Any addresses you’d like to CC on the email. You can specify multiple addresses by placing a space between each email address, just as with the -t command above.  
> * -bcc EMAIL – The BCC version of the CC option above.  

### Email Options

> * -u SUBJECT – The subject of your email  
> * -m BODY – The message body text of your email.  
> * -a ATTACHMENT – The path of a file you’d like to attach. This is optional.  

For example, let’s say your email address is you@gmail.com and you’d like to send an email to person@example.com. You’d use the following options:

```cmd
-f you@gmail.com -t person@example.com -u Subject -m This is the body text! -s smtp.gmail.com:587 -xu you@gmail.com -xp password -o tls=yes
```

Once you’ve put together your options, copy and paste them into the Add arguments box.

![SendEmails](../assets/images/windows/sendMail/sendMail4.png)

Save your task and you’re done. Your task will automatically send email on the schedule (or in response to the event) you specified.

