# Project 8 - Pentesting Live Targets

Time spent: 2 hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: SQL injections:

if we run the command :
```
' OR SLEEP (5)=0--'
```    
we see that the page takes 5 seconds to reload

Vulnerability #2: session hijacking

If we log into a browser(chrome) on the green website, we can use the hacktools to recieve a current
logged in session, and copy it so that when we go to the blue website with firefox, we can access hacktools again to change the sessionID to that of what we copied in the chrome session.
The result gives us user access within the blue website without having to be logged in manually.


## Green

Vulnerability #1: user enumeration

if we login with a correct usernname but wrong password, we get the page with the 
error class called 'failure'

however, if we login with the a nonexisting username and wrong password, we get the page with 
error class called 'failed' 



Vulnerability #2:
if we submit an xss in the feedback section, the admin can check their feedback and activate the 
xss that was subimtted by an outside user
```
<script>alert('an xss attack!');</script>
```    

## Red

Vulnerability #1: IDOR  

if we login, we can see that there is a user within salespeople that is not refferenced in the
public website. That id is 10
If we go to a persons webpage through find salesperson in the public website, we can change the id 
within the url to 10,and access that hidden user's page



Vulnerability #2:

if we create an html page that will manipulate a person's web page such as this :
```
<html>
  <body onload="document.edit_salesperson.submit()">
    <form action="https://35.184.120.185/red/public/staff/salespeople/edit.php?id=2" method="POST" name="edit_salesperson" style="display: none;" target="hidden_results" >
      <input type="text" name="first_name" value="Hacked"><br>
      <input type="text" name="last_name" value="Salesman!"><br>
      <input type="text" name="email" value="hacked@gmail.com"><br>
    </form>
    <iframe name="hidden_results" style="display: none;"></iframe>
  </body>
</html>
```
We first access the persons page with id 2, and see it is sherry trevino
while still in the same session, we launch a malicous webpage like the one above, and we reload
sherry's page and see that it is changed!

## Notes

Describe any challenges encountered while doing the work

