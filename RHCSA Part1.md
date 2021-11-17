# Welcome to my RHCSA study notes! #

## Table of contents ## 
- Lesson 1: Installation/Logging/Server requirements
- Lesson 2: Basic linux commands/Redirection I/O /Piping/File system hierarchy/globbing/wildcards/cockpit/man/vim
- Lesson 3: File management/Find/mounts/links/tar/compressed files
- Lesson 4: Common test tools/grep/regular expressions/sed&awk
- Lesson 5: Root user/virtual terminals and switching/sudo/su/ssh
- Lesson 6: User accounts and groups/create/manage their configuration files
- Lesson 7:

*I skipped Lesson 1 because there is not much to talk about here*

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Lesson 2 ### 
#### Basic linux commands ###
- `free -m` #show free memory
- `df` #show disk free
- `df -h` #show units
- `find mnt` #show mounted file systems
- `whoami` #show current username  

*_Double tab on text shows all commands starting with that text_
```
example: "fre" double tabing will show any commands starting with "fre"

```
- `history` #show all past commands done in the system

!11 #runs command no.11 in history
!f # runs last command starting with letter f

*_in history using ctrl+r will repeat previous commands_*

- `ps aux | less` #using less will show ps aux content recursively 
