
# WHAT IS SQL INJECTION?
- SQL Injection is a web security Vulnerability. 
- Used to interfere with queries that an application makes to its database.
- Can be escalated to compromise servers, back-end infrastructure and denial of service attacks.


# SQL Injection DETECTION
- There are a few methods that can be used to detect SQL Injection
- a single qoute ``` ' ``` character can be used and then you would have to search for other errors or anomalies
- Boolean conditions 
- Payloads designed to trigger time delays 
- OAST( Out of band application security testing) payloads designed to trigger an out-of-band network interaction

# SQL Injection in different parts of the query
- Most Injections occur in the ```WHERE``` Clause of a ```Select``` Query
- Sql can still occur at ANY location within the query
   # Common locations
    - ```UPDATE``` Statements within the updated values or ```WHERE``` Clause
    - ```INSERT``` Statements, within the inserted values
    - ```SELECT``` Statement, within the table or Column name
    - ```SELECT``` Statements within the ```ORDERBY clause```



# SQL Practice Lab:  SQL Injection Vulnerability in ```WHERE``` clause allowing retrieval of hidden data
 # Objective: Perform an SQL Injection attack that causes the application to display one or more unreleased products.

 1.) Open Burp Suite and manuever to the Proxy tab
 2.) Open the Browser within the proxy tab and manuever to the page where we will practice our injection
- The lab states that we are going to edit the category using an SQL injection in order to view unreleased items
- In order to do so we will turn on the burp suite interceptor so begin capturing packets and THEN select one of the category tabs
![image](https://github.com/user-attachments/assets/9ec34980-233f-4bf7-bf98-d92b88843b05)

- After doing so we will be met with the following image that shows us the GET request from the server. Just below it we can see the following line ```GET /filter?category=Clothing%2c+shoes+and+accessories HTTP/2```
- This line will be what we edit for our SQL Injection
  3.) Place Injection
- In the line mentioned above I place the following ```'+OR+1=1--```
- All the line does is state that the category should either be clothes and accessories or always true and then turns everything else after into a comment
- We then forward our change in burp suite and can see the SQL injection work on the website

# Before Completed Injection
![image](https://github.com/user-attachments/assets/3685388e-0068-4cdb-b14f-6a81c3ae3cc7)

# Injection
![image](https://github.com/user-attachments/assets/dc91a8d0-8505-47ec-b7fa-540c6ddf6544)

# After Completed Injection
![image](https://github.com/user-attachments/assets/acfb6ce3-edd9-40b5-9103-617acd3d8976)
- As you can see we are now able to several products that were previously unlisted to us before.
