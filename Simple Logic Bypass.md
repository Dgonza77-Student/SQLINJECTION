# Subverting Application Logic
In applications that allow users to log in with usernames and passwords, hackers can exploit a vulnerability where they simply analyze the SQL query say ```SELECT * FROM users WHERE username = `John` AND password = `Doe` ```

Because the query recieves ```John``` and ```Doe``` as inputs the login is success and if it does not detect those input the login fails.

All an attacker has to do is simply remove/ommit the password check after the ```WHERE``` Clause in the query

IE:

``` SELECT * FROM users WHERE username == `administrator'--` AND password = ` ` ```

The return query will be a user with the username ```Administrator``` and a successful login 


# NOTE!!!! IMPORTANT

YOU MUST USE THE '  and NOT THE ` WHEN MAKING CHANGES TO THE QUERY OR YOU WILL HAVE ISSUES

# Lab: SQL injection vulnerability allowing login bypass

- Perform a SQL injection attack that logs in to the application as the ``administrator`` user



  Here is the website as soon as we access it. We can see on the top right a ```HOME | My Account``` Area. I will use Burpsuite and turn on my interceptor when accessing the login in the ```MY account``` area. By which point I will edit the login information to bypass it.
This will allow us to perform a simple logic attack


![image](https://github.com/user-attachments/assets/7276d37f-3314-4ea7-9df1-1966f8d6e8b9)


after navigating to the ```My account``` area we see the following



![image](https://github.com/user-attachments/assets/b479f817-29ff-4be1-b3d6-712974d94e0e)

This is where we turn on the interceptor in burp suite and attempt a login

for username I place ```administrator```
for password I place ```test``` (This part will not matter but it requires you enter something)

Then I hit login


Now I look at the burp suite application which shows me the following POST request


![image](https://github.com/user-attachments/assets/d2e538c1-34cb-46d0-94d2-a587d26ff678)


At the very bottom of the POST method we can see the letters ```csrf``` and at the end ```&username=administrator&password=test```

This text will be the area of our attack.

All we simply have to do is add '-- to the end of administrator which will ommit any need for the password and simply state that all you need to access the account is the username ```administrator```


We make the quick change



![image](https://github.com/user-attachments/assets/449f2115-dbcc-4b72-9f19-ed7ad077d5ff)

And then forward the POST request
After forwarding the request, we turn off the interceptor and can see that we now have access to the account
![image](https://github.com/user-attachments/assets/113586d1-1ccb-4c1e-8c86-a213fc1eab7e)




