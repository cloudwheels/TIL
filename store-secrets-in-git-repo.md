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

