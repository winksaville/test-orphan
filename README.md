# Test Orphan

Test creating multiple DAGs on a git repo.
  https://github.com/winksaville/test-orphan

Here is the conversation I had with the bot:
  https://claude.ai/share/b8477309-bd95-4066-b22e-b987e396d392

This is the unedited set of commands mistakes an all :)

```
wink@3900x 26-05-01T15:42:54.216Z:/tmp
$ git switch --orphan test-orphan
fatal: not a git repository (or any parent up to mount point /)
Stopping at filesystem boundary (GIT_DISCOVERY_ACROSS_FILESYSTEM not set).
wink@3900x 26-05-01T15:43:51.924Z:/tmp
$ git switch --orphan test-orphan^C
wink@3900x 26-05-01T15:44:21.245Z:/tmp
$ git init test-orphan
Initialized empty Git repository in /tmp/test-orphan/.git/
wink@3900x 26-05-01T15:44:29.931Z:/tmp
$ cd test-orphan/
wink@3900x 26-05-01T15:44:32.717Z:/tmp/test-orphan (main)
$ git switch --orphan orphan1
Switched to a new branch 'orphan1'
wink@3900x 26-05-01T15:44:45.952Z:/tmp/test-orphan (orphan1)
$ git log --all --max-parents=0 --oneline
wink@3900x 26-05-01T15:45:46.184Z:/tmp/test-orphan (orphan1)
$ echo hello > a
git add a
git commit -m "root of orphan1"
git log --all --max-parents=0 --oneline
# now you'll see one entry
[orphan1 (root-commit) d21dcc0] root of orphan1
 1 file changed, 1 insertion(+)
 create mode 100644 a
d21dcc0 (HEAD -> orphan1) root of orphan1
wink@3900x 26-05-01T15:48:13.287Z:/tmp/test-orphan (orphan1)
$ git log --all --max-parents=0 --oneline
d21dcc0 (HEAD -> orphan1) root of orphan1
wink@3900x 26-05-01T15:48:16.722Z:/tmp/test-orphan (orphan1)
$ git switch main
fatal: invalid reference: main
wink@3900x 26-05-01T15:48:46.363Z:/tmp/test-orphan (orphan1)
$ echo main > a
git add a
git commit -m "root of main"
git log --all --max-parents=0 --oneline
# now you'll see one entry
[orphan1 e4c8fca] root of main
 1 file changed, 1 insertion(+), 1 deletion(-)
d21dcc0 root of orphan1
wink@3900x 26-05-01T15:53:16.923Z:/tmp/test-orphan (orphan1)
$ git log --all --max-parents=0 --oneline
d21dcc0 root of orphan1
wink@3900x 26-05-01T15:53:31.934Z:/tmp/test-orphan (orphan1)
$ git switch --orphan main
Switched to a new branch 'main'
wink@3900x 26-05-01T15:54:05.226Z:/tmp/test-orphan (main)
$ git add a^C
wink@3900x 26-05-01T15:54:19.036Z:/tmp/test-orphan (main)
$ echo main > a
git add a
git commit -m "root of main"
git log --all --max-parents=0 --oneline
# now you'll see one entry
[main (root-commit) e1df3dd] root of main
 1 file changed, 1 insertion(+)
 create mode 100644 a
e1df3dd (HEAD -> main) root of main
d21dcc0 root of orphan1
wink@3900x 26-05-01T15:54:53.039Z:/tmp/test-orphan (main)
$ gitk --all &
[2] 10457
wink@3900x 26-05-01T15:55:43.227Z:/tmp/test-orphan (main)
$ git switch orphan1
Switched to branch 'orphan1'
wink@3900x 26-05-01T15:56:13.620Z:/tmp/test-orphan (orphan1)
$ gi log --all --oneline --graph
bash: gi: command not found
wink@3900x 26-05-01T15:58:17.085Z:/tmp/test-orphan (orphan1)
$ git log --all --oneline --graph
* e1df3dd (main) root of main
* e4c8fca (HEAD -> orphan1) root of main
* d21dcc0 root of orphan1
wink@3900x 26-05-01T15:58:20.828Z:/tmp/test-orphan (orphan1)
$ git branch -v
  main    e1df3dd root of main
* orphan1 e4c8fca root of main
wink@3900x 26-05-01T15:58:32.603Z:/tmp/test-orphan (orphan1)
$ git reset --hard HEAD^
HEAD is now at d21dcc0 root of orphan1
wink@3900x 26-05-01T16:03:12.561Z:/tmp/test-orphan (orphan1)
$ git log --all --oneline --graph
* e1df3dd (main) root of main
* d21dcc0 (HEAD -> orphan1) root of orphan1
wink@3900x 26-05-01T16:03:18.521Z:/tmp/test-orphan (orphan1)
$ git reset --hard HEAD^C
wink@3900x 26-05-01T16:03:33.700Z:/tmp/test-orphan (orphan1)
$ git branch -v
  main    e1df3dd root of main
* orphan1 d21dcc0 root of orphan1
wink@3900x 26-05-01T16:03:36.566Z:/tmp/test-orphan (orphan1)
$ git log --all --oneline --graph
* e1df3dd (main) root of main
* d21dcc0 (HEAD -> orphan1) root of orphan1
wink@3900x 26-05-01T16:03:39.598Z:/tmp/test-orphan (orphan1)
$ git branch -v
  main    e1df3dd root of main
* orphan1 d21dcc0 root of orphan1
wink@3900x 26-05-01T16:03:41.716Z:/tmp/test-orphan (orphan1)
$ git switch main
Switched to branch 'main'
wink@3900x 26-05-01T16:04:33.688Z:/tmp/test-orphan (main)
$ git gui &
[3] 10797
wink@3900x 26-05-01T16:04:38.682Z:/tmp/test-orphan (main)
$ git remote add origin git@github.com:winksaville/test-orphan.git
git branch -M main
git push -u origin main
[3]+  Done                       git gui
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 431 bytes | 431.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To github.com:winksaville/test-orphan.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
wink@3900x 26-05-01T16:07:33.766Z:/tmp/test-orphan (main)
$ git switch orphan1
Switched to branch 'orphan1'
wink@3900x 26-05-01T16:07:46.174Z:/tmp/test-orphan (orphan1)
$ git push -u origin orphan1
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 435 bytes | 435.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: 
remote: Create a pull request for 'orphan1' on GitHub by visiting:
remote:      https://github.com/winksaville/test-orphan/pull/new/orphan1
remote: 
To github.com:winksaville/test-orphan.git
 * [new branch]      orphan1 -> orphan1
branch 'orphan1' set up to track 'origin/orphan1'.
wink@3900x 26-05-01T16:11:32.423Z:/tmp/test-orphan (orphan1)
```
