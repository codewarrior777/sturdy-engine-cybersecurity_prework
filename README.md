# sturdy-engine-cybersecurity_prework
Pre-work cybersecurity. Username enumeration via different responses. Brute force attack with Burp proxy
1. The Mission
The owner of a blog has contracted your security firm to test their website for vulnerabilities.

Your mission is to hack into their blog. You suspect that you can find a user whose password is too simple. First, you need to find a registered user, and then you're going to attempt dozens of different common passwords.

This would be a tedious process, but luckily, you have Burp, and its trusty Intruder tool that's built for this very purpose.

2. Setup
Install Burp - Burp is used by cybersecurity professionals everywhere to view network traffic and test for security vulnerabilities.
Create a Portswigger account - Portswigger is the maker of Burp and has an Academy to hone your cybersecurity skills.
🔗 Important Links:
Portswigger: Username Enumeration via Different responses
Portswigger: Candidate usernames
Portswigger: Candidate passwords
Step 1: Find the login url
Login to your Portswigger account
Portswigger login page screenshot
Fire up Burp, and in your Burp-configured browser:
Navigate to the blog we're targetting
Log in to your Portswigger account (yes, again!)
Once you're on the blog, navigate to the login screen
Attempt to login with a RANDOM username and password.
⚠️ The blog login looks like the image below! If you see the Portswigger login page, you should login with your Portswigger account credentials first, then it will redirect you to the blog page. Blog login page screenshot
In Burp, go to "Proxy" -> "HTTP history", and find the network request of the attempted login. You'll recognize it because it's a POST request to the login url of the blog.

Right-click the request and click "Send to Intruder"

Burp HTTP Requests screenshot
💡 Not seeing any requests? Check the intercept. "Proxy" -> "Intercept" and click the intercept button to say "Intercept is off"

 Why do we have to disable "Intercept"? (Click here for answer)
Step 2: Find a registered user
Burp Intruder allows you to make the same request over and over again, except you can specify a part of the request to change. This makes it perfect for attempting to login as many different users with thousands of passwords, known as a brute force attack.

In Burp Intruder, go to the "Positions" tab. Make sure that the attack type "Sniper" is selected.

Click "Clear" to remove any automatically assigned payload positions. In the username parameter, highlight the value and click "Add" to add a payload position to this parameter. This position will be indicated by two § symbols, for example: username=§random_username§

uIntruder
Do not change anything related to the password for now.

On the "Payloads" tab, select palyload set -> "1" and payload type -> "Simple list".

Under "Payload options", paste the list of candidate usernames and click "Start attack". The attack will start in a new window.

Username Payload
When the attack is finished, on the "Results" tab, examine the "Length" column. Click on the column header to sort the results. Notice that one of the entries is different to the other ones -- usually, 3186 is the one with a successful username.
Examine this response. Notice that other responses contain the message Invalid username, but this response says Incorrect password. Take note of this username.
If you've completed the steps above, you've identified the username of a registered user of the blog! 🎉

Although you don't know their password... yet.

⚠️ Watch out! The successful username will vary for each time you login and will only work while the session is valid. (Approx. 15 minutes). 

If the session expires, you can repeat this process to find a different username.
Step 3: Find the password
Now that you have a registered user, you want to attempt to login as that user with dozens of simple passwords.

Close the attack and go back to the "Positions" tab. Click "Clear" again and change the username parameter to the username you just identified. Add a payload position to the password parameter.Now you should see something like this username=identifiedUser&password=§invalid-password§

On the "Payloads" tab, clear the list of usernames and replace it with the list of candidate passwords. Then click "Start attack".

When the attack is finished, look at the "Status" column. Notice that each request returned a 400 status code, until eventually one returns 302. This suggests that the login attempt was successful. Take note of the password. (We covered it with a red oval so as not to spoil it for you!)

Screenshot of password attack with answer censored
Back in your browser, click the "Login" link in the upper-right corner to open a fresh login page and using the username and password that you identified. You must click "My account" to solve the lab.
🎉 Congratulations, young apprentice, you've hacked your first site! The blog owner is grateful to you for reporting a vulnerable user.
Getting an error?
Make sure you are only sending one request to the site. Sending multiple request will result in different sessions casuing a timeout error.
In general the sesssion will expire ever 15 minutes. You may need to redo the challenge if you exceed the time.
CSRF error? The CSRF token in the request is no longer valid as it was already used to succesfully login. Use a fresh login page to avoid an error.
3. Submission
👋 IMPORTANT: If you're taking this course For-Credit at your university, pre-work submission is optional.
Go to the Hall of Fame, scroll to the bottom, and take a screenshot of your entry. The bottom of the screenshot must include your username and indicate the completion of the lab with "1 of ###".
Hall of Fame
Go to GitHub and create a new repository to store your work for the class.
Add your screenshot to your repository by clicking "upload an existing file".
github
Go to the CodePath application status dashboard and then press the "SUBMIT" button in the pre-work section: Prework Submit
In the pre-work submission form, link to your GitHub repo.
