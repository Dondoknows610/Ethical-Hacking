<h1> ☁ # Ethical-Hacking👨🏿‍💻 </h1>
<h2> Description</h2>
<b>A SQL Injection demonstration as part of a series of hands on labs for ethical Hackings via Coursera.</b>
<br />


<h3>🏙 💉 SQL Injections  </h3>
<h2>Tools</h2>

- <b>Kali Linux, OWASP, Virtualbox, </b>

<h2>Program walk-through:</h2>

<p align="center">

Attackers often use many SQL injections to exploit vulnerabilities as it is one of the most effective and command methods. 
SQL Injections are capable of completely wiping out a database with DROP (luckily attackers are mostly trying to steal user names and passwords and THEN maybe delete your info lol) Bigger websites that are properly hardened such as facebook, Instragram, among others, 
are using what is called input sanitazion. This blocks the characters that are used in the syntax of an SQL injection. However, smaller websites, are often still vulnerable.

A quick lesson on the commands 
CREATE SELECT UPDATE INSERT DELETE DROP***
Super explanatory and super basic. Easy day.

<h3>Lab</h3>
THis lab is using two virtual machines, the first is the attack machine our Kali Linux. The second one is the one we are attacking our OWASP machine (Online web application security project) which is highly vulnerable and which we will exploit.

We are using our OWASP machine to host a website which is being hosted in our internal network and then accessed through the IP address via our Kali Linux machine's web browser (in this case Firefox)

On the website, once logged in, (admin, admin) ( By the way, we can also brute force these credentials via Hydra and Burpsuite) go to the left side pane menu and click the "SQL injection" link. There we find our 
input field where we can play around and inject some code.

Remember, we are logged in as the admin user, meaning we have access to this SQL database. So just to test it, it is asking for a USER ID and we will input a very simple non-malicious entry, the number 1, then the number 2, the number 3, you get the point. It works and it outputs a value for each of the ID numbers entered.

We have yet to use SQL code yet. So we will test this vulnerability by simply imputing the an apostrophe ' 

The output is an error becayse we have now broke the brain of the SQL interpreter. How?

Well, if you look at the souce code in the page below we can see that the input we put in is supposed to be interpreted by the variable $id which is sitting in between two apostrophes. So now instead of 1 we put ` meaning there are 3 apostrophes together ''' and not '1'  so that is the reason that the interpreter is confused and giving us this error. 

DIVING DEEPER 


Now we can put some code into it by putting '

This the shows that i
<img></img>


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
