<h1> 💉 # Ethical-Hacking👨🏿‍💻 </h1>
<h2> Description</h2>
<b>A SQL Injection 💉 demonstration as part of a series of hands on labs for ethical Hackings via Coursera🧪🧫 .</b>
<br />


<h3>🏙 💉 SQL Injections  </h3>

![Needle](https://github.com/user-attachments/assets/d025ebc0-8106-4af3-8e48-b398a08be535)

<h2>Tools</h2>



- <b>Kali Linux, OWASP, Virtualbox, </b>

<h2>Program walk-through:</h2>

<p align="center">

Attackers often use many SQL injections to exploit vulnerabilities as it is one of the most effective and command methods. 
SQL Injections are capable of completely wiping out a database with the command DROP (luckily attackers are mostly trying to steal user names and passwords and THEN maybe delete your info lol) Bigger websites that are properly hardened such as facebook and Instagram now are using what is called input sanitazion. This blocks the characters that are used in the syntax of an SQL injection. However, smaller websites, are often still vulnerable to these SQL Injections.

<h3>A quick lesson on the SQL commands. <h3>
These are the commands, 1. CREATE 2. SELECT 3. UPDATE 4. INSERT 5. DELETE 6. DROP (*MOST DANGEROUS ONE, CAN DELETE COMPLETE DATABASES)
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

1. We start by testing the vulnerability, we can do this by putting the symbol '

![Testing SQL with '](https://github.com/user-attachments/assets/6244c10a-c1a6-4083-bf5e-8b32f556289b)

This the shows that input field and the database is vulnerable as it interprets the symbol as part of the code.

![' input Error](https://github.com/user-attachments/assets/2cb818ae-8d3c-4076-acb7-f6a5dc6e3459)

Note: By opening the source code we can see that the ' symbol now sits between two other ' symbols and thus causing the error. Instead of having the correct query the syntax now reads 

 SELECT first_name, last_name FROM users WHERE user_id = '''

 2. Now that we know it is vulnerable we will simply add the number two to understand what the format of the output, which we can see is two distinct parts: first name and surname.

![regular input](https://github.com/user-attachments/assets/afb45415-f4ef-4614-82e4-6553b2d6254d)


  
 3.  Next we add two statements into the query as opposed to just our regular input of a single number.

![double statement i e](https://github.com/user-attachments/assets/bc768107-e1f1-4900-af33-3f09eff12b5d)


<h2>Mapping our Database and navigating with SQL Injections </h2>

![compass](https://github.com/user-attachments/assets/38bdf52a-48e8-4f31-b0d9-d0ed38c5a73a)

 4. Mapping out our database. Now we will get into our first command ORDER which will be put into our query as the second statement so we will use ORDER BY. This will help us to map out the database by helping us with listing the columns. Our syntax will then be 2' ORDER BY 2 #' where 2 is our user ID and a normal input but the ORDER BY is our SQL Injection

 Note: The hashtag is the comment indicator in html so anything after the hashtag is interpreted as a comment as opposed to code.

 ![2' order by '2](https://github.com/user-attachments/assets/5854bf8c-9d27-4213-b26d-bf16d958e07e)


4.b we will continue to map the columns by changing the 2 to a 3 so we will use 
2' ORDER BY 3 #'
Which gives us an error and we can now deduct that there are only 2 columns.

![2' ORDER BY 3 '#](https://github.com/user-attachments/assets/a3370e87-4928-4f55-be53-d292fc5e7527)

  
5. Using the UNION command to be able to gather results from two commands. We Will type 2' UNION SELECT 1,2 #' and this will give us the regular output from the user ID 2 + the order of the columns from the second statement
 ![UNION SELECT](https://github.com/user-attachments/assets/69ec8b5f-3a4b-4737-80a4-b97adbc19cd5)

6. Finding the name of the database can be done by our <b>double statement</b> which again follows the regular input of 2 <b>and</b> our second statement which will be UNION SELECT database(),user() #' so all together we have our input 2' UNION SELECT database(),user() #'
![UNION SELECT database(),user() #'](https://github.com/user-attachments/assets/34eee87e-b610-4559-bb06-4ecf63fd14c3)

7.	Next we use 2' UNION SELECT database(),user() #' which finds the name of the database and user

![UNION SELECT database(),user() #'](https://github.com/user-attachments/assets/800a31e4-a125-4a80-b1f0-bd834dc7759f)


Note: we use	() because it is the syntax for the function in the code
	We get the result in the second paragraph. We can see that the name of the databse is dvwa and dvwa@localhost is the username.

8.	Now 2' UNION SELECT schema_name,2 FROM information_schema.schemata #'
a.	The dvwa is DB for the server/application



4.	Now we query for tables to see which tables are in the dvwa DB
a.	2' UNION SELECT table_name,2 FROM information_schema.tables WHERE table_schema = 'dvwa' #'
b.	We get two tables with this query guestbook and users. So we as hackers, ethical hackers, we are more interested in the users tables
c.	Now we want to find the columns in the tables

![step 8 serverapplication](https://github.com/user-attachments/assets/4eddd3d7-1c72-46e7-8526-f202a015229e)


6.	2' UNION SELECT column_name,column_type FROM information_schema.columns WHERE table_schema='dvwa' AND table_name = 'users' #'
a.	Column names are user name, last names, first names, user id’s, passwords, avatar
b.	So from this we get the column types on the other output field which is noted in var(x) or int() which is basically the number of max characters that can be used in each column.

![column names](https://github.com/user-attachments/assets/0f33f532-2051-4c1f-98ee-ea9574e281be)


![query for tables](https://github.com/user-attachments/assets/9795fef7-ce17-4492-9ea2-90d39fcdceb5)


8.	CONCAT
a.	We will use this to be able two print first name and last name in the first name output AND user name and password in surname output

   2' UNION SELECT CONCAT(user_id, '-', first_name, ' ', last_name), CONCAT(user, ':', password) FROM dvwa.users #

![passwords](https://github.com/user-attachments/assets/b3d6d90c-787f-4933-a5a2-5845b1517c87)


c.	This gives us the username and the MD5 hash of the passwords
![MD5_hashes](https://github.com/user-attachments/assets/f4c4d35b-63fd-4b54-a8d0-1f1f085e9cdb)


9.	We then decrypt by simply googling the MD5 hash

![Googling MD5](https://github.com/user-attachments/assets/e8588f4e-81d5-419a-8e57-84c72137f3c8)

![conversionfromMD5#1](https://github.com/user-attachments/assets/6f5fd4ba-7c05-4085-b6f2-992158c42e78)

10.	![conversionfromMD5#2](https://github.com/user-attachments/assets/fcd0b445-eeb1-4526-80d9-e277d65d083f)

   
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
