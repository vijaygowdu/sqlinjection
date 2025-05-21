# EX 8
# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2
![image](https://github.com/user-attachments/assets/12e11cd7-8c9c-45fb-9596-322abfc9016d)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/user-attachments/assets/bed9767b-5b11-41ba-9238-9a51e67ac4f4)
Click on the menu Login/Register and register for an account
![image](https://github.com/user-attachments/assets/34234ec5-55eb-4f58-b60d-bc8482009998)
Click on the link “Please register here”
![image](https://github.com/user-attachments/assets/57157003-af0a-46f9-a49d-061d4ca8c946)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:
![image](https://github.com/user-attachments/assets/923055d7-a6a5-4c40-9530-12dcb9699afb)
Union-based SQL injection:
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”
After logging out, Now choose the menu as shown below:
![image](https://github.com/user-attachments/assets/e47b1a73-be7a-4c7c-84ca-dd1caa9eeaa2)
![image](https://github.com/user-attachments/assets/04d34c6f-665b-468f-9791-44ff11ac6b27)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![image](https://github.com/user-attachments/assets/afdbb2b3-2ed7-4373-b179-baaf1f436df5)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.
![image](https://github.com/user-attachments/assets/0b840f63-9cd1-4449-bbd7-46d6235e4394)

The browser url of this info page need to be modified with the url as below:
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.As it is having 5 columns the query worked fine and it provides the correct resultInstead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/user-attachments/assets/5a37df72-1140-4dea-9d7f-da1322803059)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.
Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
![image](https://github.com/user-attachments/assets/620d8d2b-bf26-45ac-981c-c09261906dff)

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
