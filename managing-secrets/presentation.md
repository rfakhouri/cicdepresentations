# Managing Secrets

---

Don't check them into your code

---

Things you shouldn't check in.

------

Passwords

------

API Keys

------

Connection Strings

------

Your deep dark secrets
```
/*
* Dear Diary
* Today I cried watching Dirty Dancing. 
* I'm crazy for swayze
*/
```

---

If you do check in secrets people will find out.  
There are tools that make this trivial to do.

------

For instance...

------

**Gitrob: Putting the Open Source in OSINT**  
_Gitrob is a tool to help find potentially sensitive files pushed to public repositories on Github._
https://github.com/michenriksen/gitrob

---

Luckily there are tools that you can integrate into your build piepline to prevent this.

------

Typically they scan for strings with high entropy values

------

https://github.com/Yelp/detect-secrets

------

https://github.com/auth0/repo-supervisor

------

https://github.com/awslabs/git-secrets

------

https://github.com/dxa4481/truffleHog

------

https://github.com/anshumanbh/git-all-secrets

---

And hey accidents happen, we are all human.

------

So come up with a plan for when it does happen.

------

Here's a sample procedure. 

------

1. Remove Secret from repo  
0. Revoke secret  
- Generate New Password  
- Revoke API Keys  
0. Evaluate Potential Impact look to your Privacy Impact Assessment (PIA) to help.  
0. Notify your Privacy Office or whoever you contact when a Privacy Breach occurs

---

You should also hold a **Blameless Post-Mortem** to determine how the secret got commited and come up with a way to ensure it doesn't happen again.

---

Strategies for Blameless Post Mortems

---

5 Whys  

Keep asking why until you find the root cause of the problem  

------

- what actions they took at what time,
- what effects they observed,
- expectations they had,
- assumptions they had made,
- and their understanding of timeline of events as they occurred.

---

References  
- https://codeascraft.com/2012/05/22/blameless-postmortems/  
- https://en.wikipedia.org/wiki/5_Whys  