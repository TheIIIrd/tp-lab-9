# tp-lab02
Studying version control systems using Git as an example.

## Tutorial

```sh
❯ export GITHUB_USERNAME=TheIIIrd
❯ export GITHUB_EMAIL=metexas109@etopys.com
❯ export GITHUB_TOKEN=dd7144610a582677aa1b5578bac3b4e2a9129928ea4d3bfc5bb22bcc16f58390
❯ alias edit=nvim
```

```sh
❯ cd ${GITHUB_USERNAME}/workspace
❯ source scripts/activate
```

```sh
❯ mkdir ~/.config
❯ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: ssh
EOF
❯ git config --global hub.protocol ssh
```

```sh
❯ mkdir projects/lab02 && cd projects/lab02
❯ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in .git/
```

```sh
❯ git config --global user.name ${GITHUB_USERNAME}
❯ git config --global user.email ${GITHUB_EMAIL}
❯ git config -e --global
❯ git remote add origin git@github.com:${GITHUB_USERNAME}/tp-lab02.git
❯ git pull origin main
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), 12.76 KiB | 12.76 MiB/s, done.
From github.com:TheIIIrd/tp-lab02
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
```

```sh
❯ touch TEST.md
❯ git status 
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        TEST.md

nothing added to commit but untracked files present (use "git add" to track)
```

```sh
❯ git add TEST.md
❯ git commit -m "added TEST.md"
[master 3c6a46e] added TEST.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 TEST.md
```

```sh
❯ git push origin master
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 323 bytes | 323.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/TheIIIrd/tp-lab02/pull/new/master
remote: 
To github.com:TheIIIrd/tp-lab02.git
 * [new branch]      master -> master
```

```sh
❯ git pull origin master
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 1018 bytes | 1018.00 KiB/s, done.
From github.com:TheIIIrd/tp-lab02
 * branch            master     -> FETCH_HEAD
   aa645c1..255da6c  master     -> origin/master
Updating aa645c1..255da6c
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore
```

```sh
❯ git log 
commit 255da6c3e2a86fe39db9b9717c9faceb1fb41fd7 (HEAD -> master, origin/master)
Author: TheIIIrd <metexas109@etopys.com>
Date:   Sun Apr 21 11:35:22 2024 +0300

    Create .gitignore

commit aa645c139ab91732fc8a30db89dad87653f327be
Author: TheIIIrd <metexas109@etopys.com>
Date:   Sun Apr 21 11:31:23 2024 +0200

    added TEST.md

commit e122f869f2ef23ac79e85859a9d55c78d36801d5 (origin/main)
Author: TheIIIrd <metexas109@etopys.com>
Date:   Sun Apr 21 11:17:41 2024 +0300

    Initial commit
```

```sh
❯ mkdir sources && mkdir include && mkdir examples
❯ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
❯ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
❯ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
❯ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
❯ edit README.md
```
