# Versionare

In cadrul laboratorului vom folosi `git` pentru versionare.

Daca nu ati mai folosit git pana acuma, va trebui sa va configurati username-ul si mail-ul cu care vreti sa
semnati viitoarele commit-uri.

```Bash
$ git config --global user.name "YOUR_USERNAME"
$ git config --global user.email "your_email@gmail.com"
```

Vom creea un nou folder si in el o sa initializam un repository.

```Bash
❯ mkdir my_git_repo
❯ cd my_git_repo
❯ touch README.md
# initializam un nou repository
❯ git init
```

Acuma o sa scrie "Hello World" in fisier si o sa facem primul nostru commit

```Bash
# Aici puteti edita fisierul cu orice vreti voi
❯ echo "Hello world" > README.md
# Urmatoarea comanda ne va afisa statusul repo-ului
❯ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md
# Facem urmatoarea operatie: Adaugam fisierul README.md in commit
❯ git add README.md
# Inregistram commit-ul
❯ git commit -m "Added README.md to the repo"
```

De fiecare data cand facem modificari, o sa folosit `git add` si `git commit`.
Pentru a afisa un log folosim `git log`.

```Bash
git log

commit 70fc4d5fe8c2bbd674a2812ef85178716c7f15ca (HEAD -> master)
Author: My Username <my_email@gmail.com>
Date:   Thu Feb 16 00:46:32 2023 +0200

    Add README.md to the repo
```

Pentru a vedea diferentele fata de ultimul commit:

```Bash

git diff HEAD HEAD^
```

Acuma, vom folosi Github pentru a stoca repository-ul online. Va trebui
sa va faceti un cont pe Github si sa creati un repository nou.

```Bash
# Adaugam un loc de stocare online, o singura data
git remote add origin git@github.com:some_repo_you_created
# Incarcam tot ce avem pe local pe online, de fiecare data cand
# vrem sa facem update la ce este online
git push -u origin master
```

Daca vreti sa aflati mai multe, va recomandam urmatorul [articol](https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/).