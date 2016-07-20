# Pulling a Git Request for Dummies like Me

This is for novice Git users like myself. This document describes my very first interaction with Git. Hope you find it useful. 
Having said I'm a novice, learning to use Git makes more sense when you have a particular task at hand than if you were just running through the 'how-to' guide

Problem :
---------
I was using package _'deconstructSigs'_ on genomic data analysed using hg18 genome build. Package function _'muts.to.sigs.input'_ is hard-coded to function on hg19 build genome data only. 

Solution : 
----------
I rewrote the function _'muts.to.sigs.input'_ to accept the genome annotation package (BSGenome from Bioconductor) as a parameter therefore making it more flexible for old data. 

Use for Git :
--------------
I wanted to create a 'Pull Request' for the code which meant contacting the author of deconstructSigs to read my suggestions and think about incorporating it into his publically available code. I didn't even know it was called a 'pull' request when I started. [This](http://kbroman.org/github_tutorial/pages/fork.html) page I found was very helpful.

Steps to 'Pull':
----------------
1. Create a GitHub account for yourself at the following webpage https://github.com/
  <br/>- Create a username : Mine is Emm13
  <br/>- Provide an email address : blah@gmail.com
  <br/>- Provide a password : pwd1234

2. Log into your GitHub page using the credentials you created above

3. Click the ![Cat Silhouette](\\emea.astrazeneca.net\UK\Alderley Park\Users 08\kwjs952\Documents\Oncotrack\R-packages\GitHub-Mark) icon in the top left-hand corner of your page which will bring up a GitHub search bar. Since I am interested in _'deconstructSigs'_, I type that in and it brings up the page https://github.com/raerose01/deconstructSigs.

4. In the topright corner of the [deconstructSigs](https://github.com/raerose01/deconstructSigs) page, you will see a 'Fork' button and if you hover over it, the button says 'Fork your own copy of https://github.com/raerose01/deconstructSigs to your account'. Click it as this makes a local copy of the code for deconstructSigs in your Git repository.

5. Now you can tinker with the copy of _deconstructSigs_ to your heart's content and the author won't bat an eyelid as his copy remains unaffected. I did my 'tinkering' on a Unix-based form of Git. Here's how. 

6. Log into your favourite Unix terminal (I use MobaXterm  at my workplace). Make sure you have Git installed. If not, you might need to refer to this page [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and will need admin rights to be able to install it on your machine. 

7. Let's assume you have Git installed. I have to type 'module load git' to initiate git on my Unix terminal. If you have to do this, then do so. Else continue. The _git_ command lists all the functions you can use to work with git and a short explanation. For a more detailed explanation of any command, use -help as always
  ```
    > module load git
    > git
    > git add -help
  ```

8. Create a directory for all your Git-work which won't interfere with any other code/programs/talks etc that you work on. Keep it clean and only use it for Git. Change directory into this location
  ```
    > cd 01_Code/Git/
  ```

9. The first step is to copy the copy (yes, recursive) of 'deconstructSigs' on your profile on Github to your local profile on Unix. You need to use the command 'clone' to copy as shown below. 
  ```  
  > git clone https://github.com/emm13/deconstructSigs.git
  ```    

10. Check the status of all your code at this starting point by using the 'status' command
  ```
   > git status
     Output:
        On branch master
        Your branch is up-to-date with 'origin/master'.
        
        Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)
        
        modified:   mut.to.sigs.input.R (red colour)
        no changes added to commit (use "git add" and/or "git commit -a")
  ```

11. Now make modifications to the code using a Unix editor of your choice (I use [_nano_](https://www.nano-editor.org/) which I find really simple and easy to use). I have introduced the parameter 'bsg' into the function 'muts.to.sigs.input' and changed all occurences of the hard-coded 'BSGenome.hg19' to 'bsg'. I have then saved the changes in the original file (that's how Git knows where to look for changes!!)

12. Use the command 'add' to add changes to your local Git repository and check the status of your file
  ```  
  > git add mut.to.sigs.input.R
  > git status
        On branch master
        Your branch is up-to-date with 'origin/master'.
        
        Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)
        modified:   mut.to.sigs.input.R (colour green)
  ```    
  
13. Now commit changes to your local repository which will register your changes as part of YOUR _'deconstructSigs'_ package at YOUR Unix profile location. You have to use the *-m* option to provide an explanation of the change you have made. This is compulsary. 
  ```
    > git commit mut.to.sigs.input.R -m "Adding parameter 'bsg' to make code accessible to earlier genome builds such as hg18"
  ```  
14. Finally, you need to sync the changes you have made to the code on your local Unix profile to that on your online Git repository (mine is https://github.com/emm13). 
  
  <br \>  a. You will have to use the command 'push' to achieve this
  
  <br \>  b. You need to tell your computer where on the interwebs to 'push' your code to. Of course, you want it back on your Git repository. You can get a link to your repository by using the 'remote' command. The parameter 'origin' is a short-hand for your Git repository as it was the 'origin' of the code. 
 
  ``` 
        > git remote -v
        origin  https://github.com/emm13/deconstructSigs.git (fetch)
        origin  https://github.com/emm13/deconstructSigs.git (push)
  ```
  
  c. Then run the _push_ command

  ```
        > git push origin
  ```
  
  d. If you see the following warning message, respond to it so it won't annoy you again. 
  ```
        warning: push.default is unset; its implicit value has changed in
        Git 2.0 from 'matching' to 'simple'. To squelch this message
        and maintain the traditional behavior, use:

        git config --global push.default matching

        To squelch this message and adopt the new behavior now, use:

        git config --global push.default simple

        When push.default is set to 'matching', git will push local branches
        to the remote branches that already exist with the same name.

        Since Git 2.0, Git defaults to the more conservative 'simple'
        behavior, which only pushes the current branch to the corresponding
        remote branch that 'git pull' uses to update the current branch.

        See 'git help config' and search for 'push.default' for further information.
        (the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
        'current' instead of 'simple' if you sometimes use older versions of Git)
  ```
  e. Respond as follows. A nice explanation for this has been provided [here](http://stackoverflow.com/questions/13148066/warning-push-default-is-unset-its-implicit-value-is-changing-in-git-2-0). 
  ```
        > git config --global push.default simple
  ```
15. You know your changes have been 'pushed' when you see the following lines inyour Unix window
    ```
    Counting objects: 4, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (4/4), 730 bytes | 0 bytes/s, done.
    Total 4 (delta 3), reused 0 (delta 0)
    To https://github.com/emm13/deconstructSigs.git
    221f5b1..949f8d1  master -> master
    ```
   
16. If you haven't added or commited any changes, you will get the following message
  ```
      > git push origin
        Everything up-to-date
  ```

17. Check on your online Git repository for the changes you have committed via Unix. (Mine had - hooray!)

18. Now you are ready to raise a _Pull Request_ with the authors of _dconstructSigs_ by clicking on the 'Pull Request' button on the top right corner of your [page](https://github.com/emm13/deconstructSigs).

19. You will be asked to write a few words explaining what the changes you propose are. It pays to be as informative as you can in this section for your own future reference. Also, be respectful as it isn't your blood, sweat and tears behind the code. 

20. Now you will have to wait until the authors get back to you on whether or not they want to incorporate your suggestions into their code. 

21. Pull Request Done!




