# Terminal-Commands
Useful terminal commands.

    Control W - remove previous word
		Control C - Cancel the line
		Control U - clear line. 
		ls -tr - sort by time in reverse where recent at bottom. Otherwise just ls -t
		ls -ltr - more specific with time stamp and everything.
		mkdir (make directory)
		rmdir file(if within file it’s not empty)
                rm -rf file(remove everything in file)  - rf stand for recursive force

		git checkout -f (go back to previous version and undo the changes)
		git mv (to change name)
		git commit -am (a = all changes, m = messages)

Move to the start of line. Ctrl + a.
2. Move to the end of line. Ctrl + e.
3. Move forward a word. Meta + f (a word contains alphabets and digits, no symbols)
4. Move backward a word. Meta + b.
    1. ctr + w delete previous word, ctr + u delete whole line.
5. Clear the screen. Ctrl + l.
6. Rails commands
    1. rails s
        1. ctrl c to shut down






Git Commands:

GitBook Review and Commands:

Chapter 1: Basics

1. Clone repo and rename : git clone <url> <newName>
2. Determine which files are in which state: git status.
    1. Use git status -s for a shorter and concise version of status.
3. To add a file, use command : echo <“whatever needs to contain in file”> > <fileName>. Eg. echo “Anh” > README
    1. To open the file and modify, use command: vim <fileName>
4. To track new files and move it to stage, use: git add <fileName or directory>. If directory, includes all files within that directory.
    1. Can also do git add * , which will staged everything.
5. Don’t want git to add automatically, use: cat .gitignore, *.[oa], *~ - ignore all files ending in .o or .a (matching pattern). Also ignore files ending with ~.
6. Want to know exactly what you changed, not just which files have been changed, use git diff instead of status: git diff
7. Ready to commit your changes, use: git commit. This command will pop up default text editor so you can enter the messages of the changes. Otherwise if short message can do: git commit -m
    1. If want to skip staging area (aka skipping git add), use git commit -a -m
8. To remove file from git: git rm <fileName>
    1. Use rm to remove file from working directory, it’ll show up under “Changes not staged for commit”. Run git rm, it’ll then staged the file’s removal. 
    2. To force removal, add -f option (If you modified file and added it to staging area already and want to remove)
    3. Keep file on working tree but remove from staging: git rm --cached <fileName>
9. Rename a file name, do: git mv <file_from> <file_to>
10. To check out all the commits you’ve made, do: git log
    1. Add, -p or -patch to show differences (patch output) introduced in each commit
    2. Add -2 to show only 2 entries or whatever number of entires you want.
    3. Add  --stat to see some abbreviated stats for each commit
    4. Add --pretty changes log output to formats other than default
        1. e.g. git log -pretty=oneline, or use short, full, and fuller options
    5. Most useful is format: git log —pretty=format:”%h - %an, %ar : %s”
        1. h = abbreviated commit hash, an =  author name, ar = author date, s = subject. (look at list for more options)
    6. Can also do git log —since=2.weeks (to get last 2 weeks)
11. Undoing things, if you want to redo that commit, make additional changes you forgot, stage them and commit again using: git commit --amend
12. To unstage a file, use: git reset HEAD <fileName>
13. To unmodified a file and go back to the original working directory, do: git checkout -- <fileName>
14. To see which remote servers you have configured, run: git remote
    1. Add option -v, which shows URL that git has stored for the shortname to be used when read/write to that remote.
15. To add a new remote Git repo, do : git remote add <shortName> <url>
16. To get data from remote projects, run: git fetch <remote or shortName>
    1. Use git pull to automatically fetch and then merge remote branch to current branch.
17. Ready to share and push it upstream, do: git push <remote> <branch>
18. To inspect a remote, do: git remote show <remote>
19. Renaming and Removing remotes, do git remote rename <from> <to> and  git remote remove <shortName>
20. List all the tags (or version Numbers), do git tag, add option -l for more detail.
21. Creating annotated tags: git tag -a <versionNumber> -m <Your message>. E.g. git tag -a v1.0 -m “First version”
    1. Tagging doesn’t impact remote servers, to do so, you have to do: git push <branch> <tagName>. Do git push <branch> --tags to push all tags to remote.
22. Creating aliases for git commands: instead of typing git commit, u can type git ci if you do git config --global alias.ci commit


Chapter 2: Git Branch Knowledge.

1. See current branches, do: git branch
2. Create new branch: git branch <name>
    1. To create new branch and switch to it at same time, add -b option, e.g. git checkout -b <name>
3. Switch branch: git checkout <name>
4. Merge branch into master -> git checkout master, then git merge <name of branch>
5. To delete the branch (e.g. after you fix and deploy the work already), do: git branch -d <name>
6. To see last commit on each branch, add option -v, eg. git branch -v
7. To filter list to branches that you have or have not yet merged into branch currently on, do: git branch --merged or --no-merged
    1. If you want to delete unmerged branch, it will fail, have to do : git branch -D <name>, capitalize D.
    2. If you want to check from another branch, do git branch --merged <name>
8. To synchronize someone’s else push, you do git fetch <name (e.g. origin)>
9. To add a remote branch, do git remote add <name you want to call> <url>
10. If you want to push to remote, you do git push <remote branch> <branch name> e.g. git push origin serverfix
    1. If you push to an HTTPS url, you will be ask for username/pass, to skip this for few mins, do git config —global credential.helper cache
    2. If you don’t want the remote to be name same as local, do: git push <remote> <localBranch:newName> 
11. When doing git fetch, you don’t have a working copy yet, to get one, do: git merge <currentBranch/remoteBranch>
12. shorthand for tracking e.g. git checkout -b <branch> <remote>/<branch> to git checkout —track <remote>/<branch>
    1. An even shorter shortcut: git checkout <branch>
    2. Set up local branch with different name than remote, do: git checkout -b <newName> <remote>/<branch>
        1. Branch serverfix set up to track remote branch serverfix from origin.
13. Set local branch to remote branch that just pulled down, or change upstream branch , do git branch -u <remote>/<branch>
14. Upstream Shorthands: git merge @{u} instead of git merge origin/master
    1. To see what tracking branches you have set up, do -vv option to git branch such as git branch -vv
        1. These are just output from the last time  you fetched from each server, to fully be update, do git fetch --all; git branch -vv
15. To delete a remote branch, do git push origin --delete serverfix (deleting serverfix branch).
16. You can take patch of one change and replay on top of another branch, this is call rebasing (similar to merge, but not), you do git rebase <branch>. eg. git checkout experiment, then git rebase master where experiment and master are branches.

