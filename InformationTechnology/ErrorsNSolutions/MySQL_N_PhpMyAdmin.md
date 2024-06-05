**MySQL Installation in Arch Linux**: https://dev.to/tinapyp/installing-and-configuring-mysql-on-arch-linux-11m1

**For PhyMyAdmin Configuration**: https://www.educative.io/answers/how-to-install-phpmyadmin-in-archlinux

- Remember to replace all `php7` to `php`, for PhpMyAdmin Configuration
- and while uncommenting:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so
```

make sure that you've commented out:

```
#LoadModule mpm_event_module modules/mod_mpm_event.so
```
