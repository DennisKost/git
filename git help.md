# **Git help**  

## **Aliases**  

### aliases (for apply permanently this aliases, insert into C:\Program Files\Git\etc\profile.d\aliases.sh and restart git bash)

cmder: added in user_aliases.cmd
in rider terminal specify cmder_init.bat

    alias g='git'  
    alias i='git init'
    alias l='git log --graph --all'
    alias lo='git log --oneline --graph --all'
    alias cl='git clone -v'
    alias conf='git config --global'
    alias confl='git config -l --global'
    alias d='git diff --U5 --color-words'
    alias a='git add -Av'
    alias ac='git add -A;git commit -v'
    alias c='git commit -v' 
    alias ca='git add -A;git commit -v --amend'
    alias co='git checkout' 
    alias com='git checkout master'  
    alias cod='git checkout dev'  
    alias chp='git cherry-pick -n'  
    alias chpcon='git cherry-pick --continue'
    alias reb='git rebase -vi'
    alias rebcon='git rebase --continue'
    alias k='gitk --all&'  
    alias st='git stash push -u'  
    alias stl='git stash list'  
    alias sta='git stash apply'  
    alias stp='git stash pop'  
    alias std='git stash drop'  
    alias r='git reset'  
    alias rhard='git reset --hard'
    alias s='git status --show-stash'
    alias b='git branch'
    alias ba='git branch -av'
    alias bdel='git branch -dv'
    alias brdel='git push -v --delete origin'
    alias m='git merge -v --no-ff --log --no-commit'
    alias mff='git merge -v --ff-only' 
    alias mcon='git merge --continue'  
    alias pl='git pull -v --rebase origin'  
    alias plm='git pull -v --rebase origin master'  
    alias pld='git pull -v --rebase origin dev'  
    alias psh='git push -uv origin'  
	alias pshall='git remote | xargs -L1 git push --all'
	alias pshallforce='git remote | xargs -L1 git push --all -f'
    alias pshforce='git push -ufv origin'  
    alias pshm='git push -uv origin master'  
    alias pshmforce='git push -ufv origin master'  
    alias pshd='git push -uv origin dev'  
    alias pshdforce='git push -ufv origin dev'  
    alias f='git fetch -pv origin'
    alias npal='/c/Program\ Files/Notepad++/notepad++.exe /c/Program\ Files/Git/etc/profile.d/aliases.sh&'
    alias dn='dotnet'  
    alias dnb='dn build'  
    alias dnb5='dn build -f net5.0'  
    alias dnb5w='dn build -f net5.0-windows'  
    alias dnr='dn run'  
    alias dnr5='dn run -f net5.0'  
    alias dnr5w='dn run -f net5.0-windows'  

### delete alias  

    unalias <alias>

## **Git extension commands** 

### set pull rebase as default

	git config --global pull.rebase true

### update git on windows  

    git update-git-for-windows

### set notepad++ as a git bash association editor  

    git config --global core.editor "'C:\Program Files\Notepad++\notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

### add bash-git-prompt (<https://github.com/magicmonty/bash-git-prompt>, config commands - <https://gist.github.com/bradwilson/7631d87b56c7e7071c6d>)  

    git clone https://github.com/magicmonty/bash-git-prompt.git ~/.bash-git-prompt --depth=1

### open configs in editor (.gitconfig directory: ~)

    git config -e --global

### edit config

	git config --global user.name "Johnny Depp"  
	git config --global user.email johnnydepp@example.com  

### delete only in index files in .gitignore

    git ls-files --cached --ignored --exclude-standard | sed 's/.*/"&"/' | xargs git rm -r --cached -- 

### move branch  

    git branch -f <branch_name> <revision>

### move branch and checkout  

    git checkout -B <branch_name> <revision>

### restore file(s) from commit  

    git checkout [<revision>] -- <file_name> [<other_file_name> [...]]

### reset hard into HEAD|branch_name from history in git reflog

    git reset --hard HEAD|branch_name@{<number>}

### get and apply last stash if lost and if it fits

    git show $stash_hash
    git stash apply $stash_hash 

### set expire time (by default gc.reflogExpire=90, gc.reflogExpireUnreachable=30, rerere.rerereResolved=60, rerere.rerereUnresolved=15)

    git config --global gc.reflogExpire <amount_of_days>.days.ago
    git config --global gc.reflogExpireUnreachable <amount_of_days>.days.ago
    git config --global rerere.rerereResolved <amount_of_days>.days.ago
    git config --global rerere.rerereUnresolved <amount_of_days>.days.ago

### set rerere to enable

    git config --global rerere.enabled true

### checkout to file without auto resolution by rerere

    git checkout --merge <file_name>

### forget rerere resolution for this file

    git rerere forget <file_name>

### rebase onto (by default [<movable_revision>]=@)

	git rebase --onto <target_revision> <beginning_revision> [<movable_revision>]

### cherry-pick if have multiple parents

	git cherry-pick -m <number_of_parent>
	
### merge with auto resolution conflicts by ours(or theirs)

	git merge --strategy-option=<ours|theirs> <revision>
	
### compare two files on disk
	
	git diff [<options>] --no-index [--] <path> <path>
	
### git diff name only

	git diff --name-only

### if have conflicts, switch to file(s) state ours or theirs

	git checkout --<outs|theirs> -- [<file1> [<file2> [...]]] 
  
### stash apply|pop|drop N stash of stash list

    git stash apply|pop|drop stash@{N}
	
### calculate numbers of line in source .cs and .xaml files in wpf projects:

	wc -l $(git ls-files | grep -e '.*\.cs$' -e '.*\.xaml$')
	Get-ChildItem -Filter "*.cs" -Recurse | Get-Content | Measure-Object -line
	
### add end of file teminator for files matching the mask

	git ls-files -z '*.cs' '*.xaml' '*.txt' '*.py' '*.cpp' '*.c' '*.h' '*.hh' '*.html' '*.js' '*.css' '*.ts' | while IFS= read -rd '' f; do tail -c1 < "$f" | read -r _ || echo >> "$f"; done

### showing unreachable commits

	git fsck --no-reflog | awk '/dangling commit/ { print $3}'| xargs -I %m git show -s --format="%h - %ci %s" %m
	
### To push all branches to all remotes

	git remote | xargs -L1 git push --all
	
### Or if you want to push a specific branch to all remotes:

	git remote | xargs -L1 -I R git push R <branch_name>

### git fame

	https://github.com/oleander/git-fame-rb
