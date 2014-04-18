---
layout: post
status: publish
published: true
title: mysqldump Command Not Working in Shell Scripts
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 809
wordpress_url: http://www.allthingsdork.com/?p=809
date: '2013-10-23 10:48:28 -0500'
date_gmt: '2013-10-23 16:48:28 -0500'
categories:
- Tech
- linkedin
tags:
- mysql
- scripting
- backups
comments: []
---
<p>I was working on a quick and dirty mysql backup script today. It was nothing complex, yet for some reason I could not for the life of me get it to execute. Here's the script in its entirety, minus the obvious redactions.</p></p>
<pre><code><br />
#!/bin/bash</p>
<p>DB=${1}<br />
USER="USER"<br />
PASS="PASSWORD"<br />
BACKUP_DIR="/tmp/sqlbackups"<br />
CMD="/usr/bin/mysqldump"<br />
DATE=`date +%Y%m%d`<br />
BACKUP_COMMAND="${CMD} -u${USER} -p'${PASS}' ${DB}"</p>
<p>echo "`date` -- Backing up database ${DB}"</p>
<p>${BACKUP_COMMAND} > ${BACKUP_DIR}/${DATE}.${DB}.sqldmp<br />
rc=$?</p>
<p>if [ $rc -eq 0 ];<br />
then<br />
    echo "`date` -- Zipping up DB"<br />
    /bin/gzip ${BACKUP_DIR}/${DATE}.${DB}.sqldmp</p>
<p>    echo "`date` -- Deleting old backups"<br />
    /bin/find ${BACKUP_DIR} -name "*${DB}.sqldmp.gz" -mtime +5 -exec rm {} \;<br />
else<br />
    echo "`date` -- Backup Failed! Aborting"<br />
fi<br />
</code></pre></p>
<p>I continuously received an "Access Denied" error message for the user. Just so I knew I wasn't crazy, I echo'd the command that was being executed, copied and pasted it and voila. Backups. WUT!?!</p></p>
<p>The current password was pretty long and contained spaces, so I figured, maybe the spaces were causing problems. I created a brand new user on sql.</p></p>
<pre><code><br />
grant select, lock tables on 'database_name'.* TO 'database_user'@'localhost' IDENTIFIED BY 'password with no spaces'<br />
</code></pre></p>
<p>Same results. Works when I copy and paste the command, but doesn't execute through the script.</p></p>
<p>So to debug the thing, I removed the -p from my command line so that I'd be prompted for a password. DISCO! It worked. <strong>WUT!?!?</strong></p></p>
<p>Now that I switched the password to be a password with no spaces, I decided for shits and giggles to remove the single quotes. Suddenly I'm in backup heaven.</p></p>
<p>I don't claim to be an expert on the evils of string variables in bash, but my understanding was that quoting the string, inside of a double quote would produce a literal single quote. Based on the output when I echo'd the command line variable, that's <strong>EXACTLY</strong> what was happening. But for some reason mysqldump just didn't care for that.</p></p>
<p>Odd, but solved. I saw a bunch of people reporting the same problem on the web with no answers, so I thought I'd post my experiences.</p></p>
