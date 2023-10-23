# SQL Injection

## Objective:
The objective of this lab is to gain hands-on experience in executing a manual SQL Injection attack against a vulnerable web application, specifically the JuiceShop application. Utilizing BurpSuite as an intercepting proxy, the goal is to trick the JuiceShop server into divulging sensitive information, such as stored usernames and passwords, without using the application's front-end login functionalities. This will be achieved by carefully constructing and injecting SQL queries into the application while monitoring and modifying the web traffic through BurpSuite.

## Walkthrough:
- I initiated the process by pulling the Juice Shop image into Docker using the command **(sudo docker pull bkimminich/juice-shop)**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/SQL%20Injection/Assets/SQL1.jpg" alt="">
</p>

- To run the Juice Shop container, I executed **(sudo docker run --rm -p 3000:3000 bkimminich/juice-shop)**. This command sets up the Juice Shop to run on port 3000 of my local machine, making it accessible via a web browser at the URL **"localhost:3000"**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/SQL%20Injection/Assets/SQL2.jpg" alt="">
</p>

- Next, I launched **BurpSuite** using the terminal with the simple command burpsuite.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/SQL%20Injection/Assets/SQL3.jpg" alt="">
</p>

- Inside BurpSuite, I accessed the Proxy Tab and used its integrated browser to navigate to **"localhost:3000"**, thereby opening Juice Shop.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/SQL%20Injection/Assets/SQL4.jpg" alt="">
</p>

- I then proceeded to the login page, where I input an email as a single quote **(')** and set the password to **"123"**. This resulted in an invalid response labeled **[object Object]**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/SQL%20Injection/Assets/SQL5.jpg" alt="">
</p>

- I returned to the **"HTTP history"** tab in BurpSuite and located the URL corresponding to my failed login attempt, which displayed a status code of 500.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/SQL%20Injection/Assets/SQL6.jpg" alt="">
</p>

- Upon examining the **"Request"** and **"Response"** logs for the failed POST, I observed an SQL query within the **"Response"** log. This suggested the possibility of executing an SQL injection attack.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/SQL%20Injection/Assets/SQL7.jpg" alt="">
</p>

- Switching over to the **"Intercept"** and **"Raw"** tabs, I inserted my chosen SQL injection payload, **(' OR '1'='1' --)**.

<p align="center">
  <img src="https://github.com/B-Johnson89/Cybersecurity-Projects/blob/main/SQL%20Injection/Assets/SQL8.jpg" alt="">
</p>

- After forwarding this payload, I checked the **"HTTP history"** tab again and discovered a new **"POST"** login request, now with a successful **200 status code**.

<p align="center">
  <img src="" alt="">
</p>

- The raw response indicated that I had successfully logged in as an admin with the email address **"admin@juice-sh.op"**.

<p align="center">
  <img src="" alt="">
</p>

- Returning to the Juice Shop in my web browser, I was greeted with a message informing me that I had successfully completed the challenge of logging in as an admin.

<p align="center">
  <img src="" alt="">
</p>
