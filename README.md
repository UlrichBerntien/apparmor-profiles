# Apparmor profiles collection

[Apparmor](https://apparmor.net/) profiles I created or optimized for my usage.

Current the profiles are used on Xubuntu 20.04.

## Ubuntu packages

The [apparmor](https://packages.ubuntu.com/focal/apparmor) package
"user-space parser utility for AppArmor" is standard in Xubuntu.
I installed also the package
[apparmor-utils](https://packages.ubuntu.com/focal/apparmor-utils) "utilities for controlling AppArmor"
and
[apparmor-profiles-extra](https://packages.ubuntu.com/focal/apparmor-profiles-extra) "Extra profiles for AppArmor Security policies".

```
apt install apparmor-utils apparmor-profiles-extra
```

## Profile development

To start with a new profile I use the aa-genprof tool according to the tips given in [apparmor>Wiki>Profiling_with_tools](https://gitlab.com/apparmor/apparmor/-/wikis/Profiling_with_tools).

```
aa-genprof <executable>
```

To test a profile: Run bash with the permissions of the profile.
```
aa-exec -p <Profilename> -- bash
```

The Profilename is the name of the profile defined inside the profile.
E.g. to test the profile stored in apparmor.d/usr.bin.transmission-gtk call:
```
aa-exec -p /usr/bin/transmission-gtk -- bash
```
The program aa-exec could be used as normal user and as root.
The tool is **not** restricted for root.

After editing a profile don't forget to replace the profile
in the kernel with "apparmor_parser -r <Profilefile>"

## Logging

The files
- rsyslog.d/30-apparmor.conf
- logrotate.d/apparmor

configure a logging of the AppArmor kernel messages into /var/log/apparmor.log with logrotation.
