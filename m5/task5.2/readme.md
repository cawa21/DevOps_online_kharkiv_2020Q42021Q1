![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/1.jpg)


/etc/passwd Format
From the above image:

Username: It is used when user logs in. It should be between 1 and 32 characters in length.
Password: An x character indicates that encrypted password is stored in /etc/shadow file. Please note that you need to use the passwd command to computes the hash of a password typed at the CLI or to store/update the hash of the password in /etc/shadow file.
User ID (UID): Each user must be assigned a user ID (UID). UID 0 (zero) is reserved for root and UIDs 1-99 are reserved for other predefined accounts. Further UID 100-999 are reserved by system for administrative and system accounts/groups.
Group ID (GID): The primary group ID (stored in /etc/group file)
User ID Info: The comment field. It allow you to add extra information about the users such as user’s full name, phone number etc. This field use by finger command.
Home directory: The absolute path to the directory the user will be in when they log in. If this directory does not exists then users directory becomes /
Command/shell: The absolute path of a command or shell (/bin/bash). Typically, this is a shell. Please note that it does not have to be a shell. For example, sysadmin can use the nologin shell, which acts as a replacement shell for the user accounts. If shell set to /sbin/nologin and the user tries to log in to the Linux system directly, the /sbin/nologin shell closes the connection.
I hope you understood /etc/passwd file format. Let us see some examples of commands.




Where,
group_name: It is the name of group. If you run ls -l command, you will see this name printed in the group field.
Password: Generally password is not used, hence it is empty/blank. It can store encrypted password. This is useful to implement privileged groups.
Group ID (GID): Each user must be assigned a group ID. You can see this number in your /etc/passwd file.
Group List: It is a list of user names of users who are members of the group. The user names, must be separated by commas.

![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/2.jpg>



Special Linux UIDs
In theory, the range of the C type uid_t is 32bit wide on Linux, i.e. 0…4294967295. However, four UIDs are special on Linux:

0 → The root super-user

65534 → The nobody UID, also called the “overflow” UID or similar. It’s where various subsystems map unmappable users to, for example file systems only supporting 16bit UIDs, NFS or user namespacing. (The latter can be changed with a sysctl during runtime, but that’s not supported on systemd. If you do change it you void your warranty.) Because Fedora is a bit confused the nobody user is called nfsnobody there (and they have a different nobody user at UID 99). I hope this will be corrected eventually though. (Also, some distributions call the nobody group nogroup. I wish they didn’t.)

4294967295, aka “32bit (uid_t) -1” → This UID is not a valid user ID, as setresuid(), chown() and friends treat -1 as a special request to not change the UID of the process/file. This UID is hence not available for assignment to users in the user database.

65535, aka “16bit (uid_t) -1” → Before Linux kernel 2.4 uid_t used to be 16bit, and programs compiled for that would hence assume that (uid_t) -1 is 65535. This UID is hence not usable either.

The nss-systemd glibc NSS module will synthesize user database records for the UIDs 0 and 65534 if the system user database doesn’t list them. This means that any system where this module is enabled works to some minimal level without /etc/passwd.



Special Distribution UID ranges
Distributions generally split the available UID range in two:

1…999 → System users. These are users that do not map to actual “human” users, but are used as security identities for system daemons, to implement privilege separation and run system daemons with minimal privileges.

1000…65533 and 65536…4294967294 → Everything else, i.e. regular (human) users.

Special systemd GIDs
systemd defines no special UIDs beyond what Linux already defines (see above). However, it does define some special group/GID assignments, which are primarily used for systemd-udevd’s device management. The precise list of the currently defined groups is found in this sysusers.d snippet: basic.conf


![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/3.jpg)
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/4.jpg)
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/5.jpg)
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/6.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/7.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/8.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/9.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/10.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/11.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/12.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/13.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/14.jp>
![alt text](https://github.com/cawa21/DevOps_online_kharkiv_2020Q42021Q1/blob/main/m5/task5.2/image/15.jp>



