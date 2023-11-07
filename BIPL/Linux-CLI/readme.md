## Welke files waarvoor in de profielen
### Login shells
```
File                        Voor wie                  Wanneer
- /etc/profile      =       alle gebruikers           alle shells
- ~/bash_profile    =       gebruikerspecifiek        alleen bash
- ~/bash_login      =       gebruikerspecifiek        alleen bash
- ~/.profile        =       gebruikerspecifiek        alle shells
```
### Non-login shells
```
File                        Voor wie                  Wanneer
- /etc/bashrc       =       alle agebruikers          interactieve bash
- ~/.bashrc         =       gebruikerspecifiek        interactieve bash 
```
## chmod
```
4   =   Read
2   =   Write
1   =   Execute
## Specials gaan voor alle andere modi bijv. 4755 voor setuid
4   =   setuid
2   =   setgid
1   =   sticky bit
```
## Outputs registreren
```
STDIN               = <
STDOUT              = >
STDERR              = 2>
STDOUT & STDERR     = >&
```
## User management
```bash
## Users aanmaken
sudo useradd -m -s /bin/bash -c "Marion Aster" master

## Password
sudo chage --maxage 40 master
sudo chage --mindays 1 master
sudo chage --warndays 7 master

## Lock account
sudo usermod -L "Marion Aster"
```
## visudo
```bash
## Allow root to run any commands anywhere
root    ALL=(ALL)       ALL

## Allows members of the 'sys' group to run networking, software,
## service management apps and more.
# %sys ALL = NETWORKING, SOFTWARE, SERVICES, STORAGE, DELEGATING, PROCESSES, LOCATE, DRIVERS

## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL

## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

## Allows members of the users group to mount and unmount the
## cdrom as root
# %users  ALL=/sbin/mount /mnt/cdrom, /sbin/umount /mnt/cdrom

## Allows members of the users group to shutdown this system
# %users  localhost=/sbin/shutdown -h now
```