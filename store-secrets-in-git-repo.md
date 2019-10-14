# Store secrets in a git repository

Use [Black Box](https://github.com/StackExchange/blackbox) to encrypt secrets (API keys etc) for storing in a repo.

## Install by making .deb package

- Install fpm

- Clone repo & cd

(from home directory)

`git clone https://github.com/StackExchange/blackbox.git && cd blackbox`

- Make .deb package

`make packages-deb`
```
sed -e '/^#/d' -e 's@/usr/blackbox/bin/@/usr/bin/@g' -e '/profile.d-usrblackbox.sh/d' <tools/mk_rpm_fpmdir.stack_blackbox.txt >tools/mk_deb_fpmdir.stack_blackbox.txt
cd tools && OUTPUTDIR="/home/nigel/debbuild-stack_blackbox" PKGRELEASE="${PKGRELEASE}" PKGDESCRIPTION="Safely store secrets in git/hg/svn repos using GPG encryption" ./mk_deb_fpmdir stack_blackbox mk_deb_fpmdir.stack_blackbox.txt
Using /home/nigel/debbuild-stack_blackbox for OUTPUTDIR instead of /home/nigel/debbuild-stack_blackbox
epoch in Version is set {:epoch=>"0", :level=>:warn}
Debian packaging tools generally labels all files in /etc as config files, as mandated by policy, so fpm defaults to this behavior for deb packages. You can disable this default behavior with --deb-no-default-config-files flag {:level=>:warn}
Created package {:path=>"stack-blackbox_1.0-489_all.deb"}
/home/nigel/debbuild-stack_blackbox/stack-blackbox_1.0-489_all.deb
```
- Package (e.g. `stack-blackbox_1.0-489_all.deb` ) created in `~/debbuild-stack_blackbox` can be stored for distribution

- Repo can be deleted

`cd .. && rm -rf blackbox`

- Install debian package, e.g.

`sudo dpkg -i debbuild-stack_blackbox/stack-blackbox_1.0-489_all.deb`
```
Selecting previously unselected package stack-blackbox.
(Reading database ... 82767 files and directories currently installed.)
Preparing to unpack .../stack-blackbox_1.0-489_all.deb ...
Unpacking stack-blackbox (1.0-489) ...
Setting up stack-blackbox (1.0-489) ...
```

## Create gpg key

See [Github instructions](https://help.github.com/en/articles/generating-a-new-gpg-key

- GnuPG is part of Debian
- Your GPG key must use RSA with a key size of 4096 bits. To generate an key pair:
```gpg --full-generate-key
```
```
gpg (GnuPG) 2.1.18; Copyright (C) 2017 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 
```
 - Enter `1`
 ```
 RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 
```
- Enter `4096`
```
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```
- Enter `0`
```
Key does not expire at all
Is this correct? (y/N) 
```
- Enter `y`
```
GnuPG needs to construct a user ID to identify your key.

Real name: 
```
- Enter your `name`, `email` and [optional] `comment`
```
Real name: Nigel
Email address: nigel@cloudwheels.net
Comment: For Blackbox
You selected this USER-ID:
    "Nigel (For Blackbox) <nigel@cloudwheels.net>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? 
```
- Enter `O`
```

                                               lqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqk
                                               x Please enter the passphrase to                       x
                                               x protect your new key                                 x
                                               x                                                      x
                                               x Passphrase: ________________________________________ x
                                               x                                                      x
                                               x       <OK>                              <Cancel>     x
                                               mqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqqj


```
- Enter, hit `return` then re-enter your **secret** `passphrase`
```
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
```
- Make some random actions as suggested

THE KEYS WILL BE GENERATED AND ADDED TO YOUR PUBLIC & PRIVATE KEYRINGS

```
gpg: key 0E81F6E4E7CE4BD5 marked as ultimately trusted
gpg: directory '/home/nigel/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/nigel/.gnupg/openpgp-revocs.d/54629BAC8EF72D2709E32A3C0E81F6E4E7CE4BD5.rev'
public and secret key created and signed.

pub   rsa4096 2019-10-14 [SC]
      54629BAC8EF72D2709E32A3C0E81F6E4E7CE4BD5
      54629BAC8EF72D2709E32A3C0E81F6E4E7CE4BD5
uid                      Nigel (For Blackbox) <nigel@cloudwheels.net>
sub   rsa4096 2019-10-14 [E]
```
### Useful sources on understanding / using GPG Keys:

https://www.tutonics.com/2012/11/gpg-encryption-guide-part-1.html

## Encrypting files in the repo

E.g. Create a sample repo & text file

`$ mkdir blackbox-test && cd $_`

`$ echo "This is a secret" > test.txt`

`$ git init && git add . && git commit -m "intial commit"`
```
Initialized empty Git repository in /home/nigel/blackbox-test/.git/
[master (root-commit) f672842] intial commit
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
 ```
### Initialise repo to use blackbox

`$ blackbox_initialize`
```
Enable blackbox for this git repo? (yes/no) y
VCS_TYPE: git


NEXT STEP: You need to manually check these in:
      git commit -m'INITIALIZE BLACKBOX' .blackbox /home/nigel/blackbox-test/.gitignore
```
`$ git commit -m'INITIALIZE BLACKBOX' .blackbox /home/nigel/blackbox-test/.gitignore`
```
[master 89d89dc] INITIALIZE BLACKBOX
 3 files changed, 3 insertions(+)
 create mode 100644 .blackbox/blackbox-admins.txt
 create mode 100644 .blackbox/blackbox-files.txt
 create mode 100644 .gitignore
 ```
 ### Add admins / keys to the repo

`blackbox_addadmin <gpg-key>`

e.g.

`$ blackbox_addadmin 0E81F6E4E7CE4BD5`
```
gpg: keybox '/home/nigel/blackbox-test/.blackbox/pubring.kbx' created
gpg: /home/nigel/blackbox-test/.blackbox/trustdb.gpg: trustdb created
gpg: key 0E81F6E4E7CE4BD5: public key "Nigel (For Blackbox) <nigel@cloudwheels.net>" imported
gpg: Total number processed: 1
gpg:               imported: 1


NEXT STEP: You need to manually check these in:
      git commit -m'NEW ADMIN: 0E81F6E4E7CE4BD5' .blackbox/pubring.kbx .blackbox/trustdb.gpg .blackbox/blackbox-admins.txt
```
`git commit -m'NEW ADMIN: 0E81F6E4E7CE4BD5' .blackbox/pubring.kbx .blackbox/trustdb.gpg .blackbox/blackbox-admins.txt`
```
[master 5a09d20] NEW ADMIN: 0E81F6E4E7CE4BD5
 3 files changed, 1 insertion(+)
 create mode 100644 .blackbox/pubring.kbx
 create mode 100644 .blackbox/trustdb.gpg
 ```
 
 ### Register / Encrpyt file
 
 `$ blackbox_register_new_file test.txt`
```
========== PLAINFILE test.txt
========== ENCRYPTED test.txt.gpg
========== Importing keychain: START
gpg: Total number processed: 1
gpg:              unchanged: 1
========== Importing keychain: DONE
========== Encrypting: test.txt
========== Encrypting: DONE
========== Adding file to list.
========== CREATED: test.txt.gpg
========== UPDATING REPO:
rm 'test.txt'
NOTE: "already tracked!" messages are safe to ignore.
[master aeac05b] registered in blackbox: test.txt
 3 files changed, 2 insertions(+)
 create mode 100644 test.txt.gpg
========== UPDATING VCS: DONE
Local repo updated.  Please push when ready.
    git push
```

The file will be encrpted (.gpg extension added)...

`$ ls`

`test.txt.gpg`

and contain gobbledegook!

`cat test.txt.gpg`
```
�
 ��?�Z v���N�7� ��5�ѪG��ɚU>��˾ ��fܻ��p���pi"b���p���)3q
�����!I�w�?�=yt�OA;y
���o=b�
3A�;A�ڗT#h�(�mk���Y���g����kÔ�s�ҵ0�Ō��kE4VNw^����0V�h�5P*��={]���*h�l���~z"J��h�9hq"    �.0ݟ�Ӆʨ�^�:�5�>��~?��[���fp&�6d̯�d�b���:]v� ��H�X/�Q���.����1
���!���'a���t�΢���Cq�E����`�q�g�a.�/�f���Ů�6�'U�凊�x���?�AK�ڇǩ�<�~~ߢV�^=�S����s$�΅�4�2����s�ۺ��^s�!GٍF)��n�]9+�7"a�k�
ͫ@�[��1��XԤ
```
