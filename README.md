
### How to setup server to use this utility
1. Add DNS records:
  - MX     5  mail.yourdomain.com
  - A   mail  42.42.42.42

2. install Python

```
> pkg install python
```

3. upload this program

```
$ rsync -p weblog you@yourdomain.com:/path/to/this/program
```

4. add Sendmail alias

This will configure Sendmail to turn emails addressed to editor@yourdomain.com into weblog posts for the user "richard".

```
> cp /ect/mail/aliases.sample /etc/mail/aliases
> echo 'editor: "| /path/to/this/program richard"' >> /etc/mail/aliases
> newaliases
```

5. add Sendmail access rule

```
> echo 'From:mail.my-email-provider.com  OK' >> /etc/mail/access
> makemap hash /etc/mail/access < /etc/mail/access
> service sendmail restart
```

6. create $(HOME)/weblog/static/posts directory

```
$ mkdir weblog
$ chgrp mailnull weblog
$ chmod g+wx weblog/static/posts
```
