# tf2recompiled-public
Patches for Team Fortress 2's leaked source code <br>
The private version is for some commits patches that I can't share yet such as for a video <br>
When I will be able to, I'll share the patches in this repo <br>

## Creating a Git repo
Note: Creating a Git repo is not required just to apply patch but I still recommend it since it only takes 5 minutes or so <br>
If you don't know what a Git repo is, click <a href="https://www.youtube.com/watch?v=hwP7WQkmECE&ab_channel=Fireship">here</a> <br>
<br>
Before creating the repo, make sure you don't already have a `.git` directory in your project, if you do, that means you already have a repo <br>
If you want to create a new one, delete the directory <br>
<br>
So first, type `git init` in your project directory (parent of hl2_src) <br>
This will create the Git repo but you're not done yet, you need a `.gitignore` file (you might already have one but it's missing some stuff so use the file named `recommended.gitignore` in this Github repo and rename it to `.gitignore`) <br>
Then you need to create an Initial commit (see the "Creating a patch" section for a deeper explanation) <br>
To do that, type `git add hl2-src` and `git commit -m "Initial commit"` <br>
<br>
You can then make changes some files and create a patch! (see the "Creating a patch" section) <br>

## Creating a patch
To create a patch, make sure you have a `.git` directory in your project <br>
If you don't, see the "Creating a Git repo" section <br>
Then make the changes to whatever files you want and when you're done, type `git status` <br>
It should say something like <br>
```diff
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
-       modified:   hl2_src/game/server/tf/tf_player.cpp
-       modified:   hl2_src/game/shared/tf/tf_player_shared.cpp
-       modified:   hl2_src/game/shared/tf/tf_shareddefs.cpp
-       modified:   hl2_src/game/shared/tf/tf_shareddefs.h
-       modified:   hl2_src/game/shared/tf/tf_weaponbase.cpp
-       modified:   hl2_src/game/shared/tf/tf_weaponbase_gun.cpp
-       modified:   hl2_src/game/shared/tf/tf_weaponbase_melee.cpp
-       modified:   hl2_src/game/shared/tf/tf_obj_catapult.cpp

no changes added to commit (use "git add" and/or "git commit -a")
```
Use `git add path/to/the/files` to tell Git you want to include them in your patch <br>
After that, you can use `git status` again and it should answer something like <br>
```diff
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
+       modified:   hl2_src/game/server/tf/tf_player.cpp
+       modified:   hl2_src/game/shared/tf/tf_player_shared.cpp
+       modified:   hl2_src/game/shared/tf/tf_shareddefs.cpp
+       modified:   hl2_src/game/shared/tf/tf_shareddefs.h
+       modified:   hl2_src/game/shared/tf/tf_weaponbase.cpp
+       modified:   hl2_src/game/shared/tf/tf_weaponbase_gun.cpp
+       modified:   hl2_src/game/shared/tf/tf_weaponbase_melee.cpp
-       modified:   hl2_src/game/shared/tf/tf_obj_catapult.cpp
```
The files in green will be included in the patch <br>
The files in red won't <br>
If you included a file by accident, you can use `git restore path/to/the/files` to remove it <br>

Once you're sure your patch is ready, type `git commit -m "The name of the commit, this will be the name of the patch"` and `git format-patch -1` <br>
The first command will commit the changes to the Git repo and the second command will create a .patch file from your last commit <br>
The file will have a number before its name (for example: `0001-Epic-commit`), you can just rename the file to remove them <br>
You can then upload the patch using the Github interface <br>
<br>
If you want to go back to a previous commit, you'll need its ID <br>
You can find it using `git log`, a command that will show all commits you've made <br>
Then, copy the ID of the commit you want to go back to <br>
There are multiple ways of going back to an old commit, the ones I mostly use are: <br>
- `git checkout` <br>
  If you use `git checkout` to restore an old commit, it will actually create another commit so you can still go back to the state before restoring <br>
  To go back to the old commit, type `git checkout your_commit_id`, `git add .` and `git commit -m "Reverting to your_commit_id_or_your_commit_name"` <br>
  Your old commit should have been restored! <br>
  <br>
  You can also use:
  <br>
- `git reset --hard` <br>
  `git reset --hard` will <b>delete</b> every commit after the old one <br>
  So be very careful when using this method <br>
  <br>
  The command to reset to a commit is just `git reset --hard your_commit_id`, without any confirmation, <br>
  so make really sure you're going back to the right commit <br>
<br>
Once your patch has been created, you can apply it easily, check the "Applying a patch" section <br>

## Applying a patch
Applying a patch is a really simple command: `git am < file.patch` <br>
If you have created a Git repo, a commit will be created
