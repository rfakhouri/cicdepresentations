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
* I'm crazy for Swayze
*/
```

---

If you do check in secrets people will find out.  
There are tools that make this trivial to do.

------

For instance...

------

**Gitrob**  

Gitrob is a tool to help find potentially sensitive files pushed to public repositories on Github.

https://github.com/michenriksen/gitrob

---

Luckily there are tools that you can integrate into your build pipeline to prevent this.

------

Typically they scan for strings with high entropy values and common phrases such as `password`, `username`, well known files names such as `.env`, and other things that people who are cleverer then me have thought of. 

------

**Detect Secrets**  

However, unlike other similar packages that solely focus on finding secrets, this package is designed with the enterprise client in mind: providing a backwards compatible, systematic means of:

- Preventing new secrets from entering the code base,
- Detecting if such preventions are explicitly bypassed, and
- Providing a checklist of secrets to roll, and migrate off to a more secure storage.

https://github.com/Yelp/detect-secrets

------

**Repo Supervisor**  

Serverless tool that detects secrets and passwords in your pull requests - one file at a time.  

https://github.com/auth0/repo-supervisor

------

**Git Secrets**

Uses Git Hooks to prevent commits of secrets before the secrets get pushed to a remote repo.

https://github.com/awslabs/git-secrets

Note: Mainly used for AWS Credentials

------

**truffleHog**

Searches through git repositories for secrets, digging deep into commit history and branches. This is effective at finding secrets accidentally committed.

https://github.com/dxa4481/truffleHog

------

**Git All Secrets** 

A tool to capture all the git secrets by leveraging multiple open source git searching tools

https://github.com/anshumanbh/git-all-secrets

---

And hey accidents happen, we are all human.

------

So come up with a plan for when it does happen.

------

Here's a sample procedure. 

------

0. Remove Secret from repo  
    - Instructions for removing secrets from a Git https://help.github.com/en/articles/removing-sensitive-data-from-a-repository
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