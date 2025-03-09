<h1> ☁ # Ethical-Hacking👨🏿‍💻 </h1>
<h2> Description</h2>
<b>A SQL Injection demonstration as part of a series of hands on labs for ethical Hackings via Coursera.</b>
<br />


<h3>🏙 💉 SQL Injections  </h3>

![Needle](https://github.com/user-attachments/assets/d025ebc0-8106-4af3-8e48-b398a08be535)

<h2>Tools</h2>



- <b>Kali Linux, OWASP, Virtualbox, </b>

<h2>Program walk-through:</h2>

<p align="center">

Attackers often use many SQL injections to exploit vulnerabilities as it is one of the most effective and command methods. 
SQL Injections are capable of completely wiping out a database with the command DROP (luckily attackers are mostly trying to steal user names and passwords and THEN maybe delete your info lol) Bigger websites that are properly hardened such as facebook and Instagram now are using what is called input sanitazion. This blocks the characters that are used in the syntax of an SQL injection. However, smaller websites, are often still vulnerable to these SQL Injections.

<h3>A quick lesson on the commands <h3>
These are the commands, CREATE SELECT UPDATE INSERT DELETE DROP***
As you can see, they are all self-explanatory and super basic.

<h3>Lab</h3>
This lab is using two virtual machines, the first is the attack machine, our Kali Linux. The second one is the one we are attacking, our OWASP machine (Online web application security project), which is highly vulnerable and which we will exploit.
<tr></tr>

![Kali Linux Desktop](https://github.com/user-attachments/assets/d76ffed0-8680-4691-8016-2015f85eb423)
![Homescreen OWASP](https://github.com/user-attachments/assets/2086b00b-7279-420e-8323-5628f3ce9103)


We are using our OWASP machine to host a website which is being hosted in our internal network and then accessed through its IPV4 address via our Kali Linux machine's web browser (in this case Firefox).

On the website, once logged in with the credentials of user name: admin and password: admin, (by the way, we can also brute force these credentials via Kali Linux with our command line tools, Hydra and Burpsuite) go to the left side pan menu and click the "SQL injection" link. There we find our input field where we can play around and inject some code.

![Login DVWA](https://github.com/user-attachments/assets/b947824a-2eeb-47ea-889c-243f4390aea5)
![Pan Menu](https://github.com/user-attachments/assets/8a72230c-d7e9-404f-92e9-4e4f9384ec1f)



Remember, we are logged in as the admin user, meaning we have access to this SQL database. So just to test it, it is asking for a USER ID and we will input a very simple non-malicious entry, the number 1, then the number 2, the number 3, you get the point. It works and it outputs a value for each of the ID numbers entered.

We have yet to use SQL code yet. So we will test this vulnerability by simply imputing the an apostrophe ' 

The output is an error becayse we have now broke the brain of the SQL interpreter. How you ask?

Well, if you look at the souce code in the page below we can see that the input we put in is supposed to be interpreted by the variable $id which is sitting in between two apostrophes. So now instead of 1 we put ` meaning there are 3 apostrophes together ''' and not '1'  so that is the reason that the interpreter is confused and giving us this error. 

<h3>Diving Deeper</h3> 

Now we can put some code into it by putting the symbol '

![Testing SQL with '](https://github.com/user-attachments/assets/6244c10a-c1a6-4083-bf5e-8b32f556289b)

This the shows that input field and the database is vulnerable as it interprets the symbol as part of the code

![' input Error](https://github.com/user-attachments/assets/2cb818ae-8d3c-4076-acb7-f6a5dc6e3459)


</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
