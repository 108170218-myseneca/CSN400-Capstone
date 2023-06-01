# Checkpoint3 Submission

- **COURSE INFORMATION: CSN400-2234**
- **STUDENT’S NAME: Soufiane Berni**
- **STUDENT'S NUMBER: 108170218**
- **GITHUB USER ID: 108170218-myseneca**
- **TEACHER’S NAME: Atoosa Nasiri**

### Table of Contents
    - [PartA - Conflict Management - Overwriting Remote Changes](#PartA---conflict-management---overwriting-remote-changes)
    - [PartB - Conflict Management - Resetting Local Commit Head](#PartB---conflict-management---resetting-local-commit-head)
    - [PartC - Conflict Management - Merge Editor](#PartC---conflict-management---merge-editor)
    - [PartD - Collaboration - Creating a Pull Request](#PartD---collaboration---creating-a-pull-request)
    - [Pull Request](#pull-request)

### PartA - Conflict Management - Overwriting Remote Changes
Under the `Checkpoin3` i have created a subfolder `conflict-resolution` 
and added files into it. then i have `push` the changes. What color will the text appear? from `red` to `green`

- `* part1-conflict-error.log`

```
Pushing to https://github.com/108170218-myseneca/CSN400-Capstone.git
To https://github.com/108170218-myseneca/CSN400-Capstone.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/108170218-myseneca/CSN400-Capstone.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
- `* part1-conflict-overwrite.log`

```
POST git-receive-pack (12100 bytes)
remote: Resolving deltas:   0% (0/18)        
remote: Resolving deltas:   5% (1/18)        
remote: Resolving deltas:  11% (2/18)        
remote: Resolving deltas:  16% (3/18)        
remote: Resolving deltas:  22% (4/18)        
remote: Resolving deltas:  27% (5/18)        
remote: Resolving deltas:  33% (6/18)        
remote: Resolving deltas:  38% (7/18)        
remote: Resolving deltas:  44% (8/18)        
remote: Resolving deltas:  50% (9/18)        
remote: Resolving deltas:  55% (10/18)        
remote: Resolving deltas:  61% (11/18)        
remote: Resolving deltas:  66% (12/18)        
remote: Resolving deltas:  72% (13/18)        
remote: Resolving deltas:  77% (14/18)        
remote: Resolving deltas:  83% (15/18)        
remote: Resolving deltas:  88% (16/18)        
remote: Resolving deltas:  94% (17/18)        
remote: Resolving deltas: 100% (18/18)        
remote: Resolving deltas: 100% (18/18), completed with 1 local object.        
Pushing to https://github.com/108170218-myseneca/CSN400-Capstone.git
To https://github.com/108170218-myseneca/CSN400-Capstone.git
 + 7f5ae37...ec34eb4 main -> main (forced update)
updating local tracking ref 'refs/remotes/origin/main'
```


### PartB - Conflict Management - Resetting Local Commit Head
What color will the text be after forcefully overwriting remote changes with local changes? After modifying on `GitHub` the color for `red` to `marron`, 
then i created conflict by updating the color in (local repo) to `darkolivegreen`

- `* part2-conflict-error.log`

```
Pushing to https://github.com/108170218-myseneca/CSN400-Capstone.git
To https://github.com/108170218-myseneca/CSN400-Capstone.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/108170218-myseneca/CSN400-Capstone.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
- `* part2-pull-error.log`

```
POST git-upload-pack (196 bytes)
POST git-upload-pack (983 bytes)
From https://github.com/108170218-myseneca/CSN400-Capstone
   ec34eb4..bb98b06  main        -> origin/main
 = [up to date]      feat-emojis -> origin/feat-emojis
Auto-merging checkpoint3/conflict-resolution/index.html
CONFLICT (content): Merge conflict in checkpoint3/conflict-resolution/index.html
Automatic merge failed; fix conflicts and then commit the result.
```

- `* part2-reset-head.log`

```
HEAD is now at ec34eb4 modifies style color in index.html to green
commit ec34eb41bdc92be96e71dca28dcde7259bd93cb9
Author: 108170218-myseneca <sberni@myseneca.ca>
Date:   Sun May 28 21:49:53 2023 -0400

    modifies style color in index.html to green
```

- `* part2-pull-success.log`

```
POST git-upload-pack (196 bytes)
From https://github.com/108170218-myseneca/CSN400-Capstone
 = [up to date]      main        -> origin/main
 = [up to date]      feat-emojis -> origin/feat-emojis
Updating ec34eb4..bb98b06
Fast-forward
 checkpoint3/conflict-resolution/index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```
- `* part3-status.log`

```
On branch main
Your branch is up to date with 'origin/main'.

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
	modified:   checkpoint3/conflict-resolution/index.html
```
### PartC - Conflict Management - Merge Editor
Managing the conflict using the `VSCode` I have `Accept Incoming` and `Accept Current` for the second part. Once i have accepted both changes 
towards `Complete Merge` 

- The updated name and email in HTML
  ```
  <footer>
  <p>Author: Soufiane Berni</p>
  <p><a href="mailto:sberni@myseneca.ca"></a>sberni@myseneca.ca</p>
  <p><a href="https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts">Git Merge Conflicts</a></p>
  </footer>
</html>
```
![Finalmerge](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/checkpoint3/Finalmerge.JPG)


### PartD - Collaboration - Creating a Pull Request
After runing `git status` it showed the result below
```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```
### Pull Request
![pullrequest](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/checkpoint3/pullrequest.jpg)
