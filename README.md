<h1>💉 Ethical-Hacking 👨🏿‍💻</h1>

<h2>Description</h2>
<p><b>A SQL Injection 💉 demonstration as part of a series of hands-on labs for Ethical Hacking via Coursera 🧪🧫.</b></p>

<h3>🏙💉 SQL Injections</h3>
<img src="https://github.com/user-attachments/assets/d025ebc0-8106-4af3-8e48-b398a08be535" alt="Needle">

<h2>Tools</h2>
<ul>
  <li><b>Kali Linux, OWASP, Virtualbox</b></li>
</ul>

<h2>Program Walk-through</h2>
<p align="center">
  Attackers often use SQL injections to exploit vulnerabilities as it is one of the most effective and common methods. SQL injections can completely wipe out a database with the command <code>DROP</code> (luckily, attackers mostly try to steal usernames and passwords first, and maybe delete your info later). Larger websites like Facebook and Instagram have hardened systems using input sanitization, which blocks characters used in SQL injections. However, smaller websites often remain vulnerable.
</p>

<h3>A Quick Lesson on SQL Commands</h3>
<p>
  Here are some basic SQL commands:
  <ul>
    <li><code>CREATE</code></li>
    <li><code>SELECT</code></li>
    <li><code>UPDATE</code></li>
    <li><code>INSERT</code></li>
    <li><code>DELETE</code></li>
    <li><code>DROP</code> (most dangerous, can delete entire databases)</li>
  </ul>
</p>

<h3>Lab Setup</h3>
<p>
  This lab involves two virtual machines: the first, Kali Linux (our attack machine), and the second, the OWASP machine (Online Web Application Security Project), which is highly vulnerable and will be exploited.
</p>

<p>
  <img src="https://github.com/user-attachments/assets/d76ffed0-8680-4691-8016-2015f85eb423" alt="Kali Linux Desktop">
  <img src="https://github.com/user-attachments/assets/2086b00b-7279-420e-8323-5628f3ce9103" alt="Homescreen OWASP">
</p>

<p>
  We use the OWASP machine to host a website in our internal network, accessed via its IPV4 address through Kali Linux’s browser (Firefox). After logging in with the credentials <code>admin</code>/<code>admin</code> (which can also be brute-forced via tools like Hydra and Burp Suite), we navigate to the "SQL Injection" section via the left-side menu to test for vulnerabilities.
</p>

<p>
  <img src="https://github.com/user-attachments/assets/b947824a-2eeb-47ea-889c-243f4390aea5" alt="Login DVWA">
  <img src="https://github.com/user-attachments/assets/8a72230c-d7e9-404f-92e9-4e4f9384ec1f" alt="Pan Menu">
</p>

<p>
  We input a simple, non-malicious entry (the number 1) into the user ID field, and the system outputs a value. When we enter an apostrophe <code>'</code>, we cause an error in the SQL interpreter. The source code reveals that the input is being processed between two apostrophes, breaking the SQL syntax and leading to an error.
</p>

<h3>Diving Deeper</h3>
<ol>
  <li>
    Test the vulnerability by inputting the symbol <code>'</code>.
    <img src="https://github.com/user-attachments/assets/6244c10a-c1a6-4083-bf5e-8b32f556289b" alt="Testing SQL with '">
    <img src="https://github.com/user-attachments/assets/2cb818ae-8d3c-4076-acb7-f6a5dc6e3459" alt="Input Error">
  </li>
  <li>
    Now add the number 2 to the input to understand the output format (first name and surname).
    <img src="https://github.com/user-attachments/assets/afb45415-f4ef-4614-82e4-6553b2d6254d" alt="Regular input">
  </li>
  <li>
    Next, we use two statements in the query.
    <img src="https://github.com/user-attachments/assets/bc768107-e1f1-4900-af33-3f09eff12b5d" alt="Double statement input">
  </li>
</ol>

<h2>Mapping our Database with SQL Injections</h2>
<img src="https://github.com/user-attachments/assets/38bdf52a-48e8-4f31-b0d9-d0ed38c5a73a" alt="Compass">

<ol>
  <li>
    Map the database using the <code>ORDER BY</code> command.
    <img src="https://github.com/user-attachments/assets/5854bf8c-9d27-4213-b26d-bf16d958e07e" alt="ORDER BY">
  </li>
  <li>
    Continue mapping by adjusting the number after <code>ORDER BY</code>.
    <img src="https://github.com/user-attachments/assets/a3370e87-4928-4f55-be53-d292fc5e7527" alt="ORDER BY Error">
  </li>
  <li>
    Use the <code>UNION</code> command to combine the results of two queries.
    <img src="https://github.com/user-attachments/assets/69ec8b5f-3a4b-4737-80a4-b97adbc19cd5" alt="UNION SELECT">
  </li>
  <li>
    Find the database and user by using the query: <code>2' UNION SELECT database(), user() #</code>.
    <img src="https://github.com/user-attachments/assets/34eee87e-b610-4559-bb06-4ecf63fd14c3" alt="Database and User Info">
  </li>
</ol>

<h3>Querying for Tables</h3>
<ol>
  <li>
    Query for tables in the <code>dvwa</code> database.
    <img src="https://github.com/user-attachments/assets/007927a4-3800-430c-a72a-1dce1a4df6b1" alt="Query for Tables">
  </li>
  <li>
    Query for columns in the <code>users</code> table.
    <img src="https://github.com/user-attachments/assets/0f33f532-2051-4c1f-98ee-ea9574e281be" alt="Column Names">
  </li>
</ol>

<h3>Extracting Data</h3>
<ol>
  <li>
    Use <code>CONCAT</code> to combine first name, last name, username, and password.
    <img src="https://github.com/user-attachments/assets/b3d6d90c-787f-4933-a5a2-5845b1517c87" alt="Concatenated Data">
  </li>
  <li>
    The result includes MD5 hashes of the passwords.
    <img src="https://github.com/user-attachments/assets/f4c4d35b-63fd-4b54-a8d0-1f1f085e9cdb" alt="MD5 Hashes">
  </li>
  <li>
    Decrypt the MD5 hashes using an online tool.
    <img src="https://github.com/user-attachments/assets/e8588f4e-81d5-419a-8e57-84c72137f3c8" alt="Googling MD5">
    <img src="https://github.com/user-attachments/assets/6f5fd4ba-7c05-4085-b6f2-992158c42e78" alt="Conversion from MD5 #1">
    <img src="https://github.com/user-attachments/assets/fcd0b445-eeb1-4526-80d9-e277d65d083f" alt="Conversion from MD5 #2">
  </li>
</ol>
