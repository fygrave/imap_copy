IMAP Copy
=========

This is a very simple tool to copy folders from one IMAP server to another server.


Example:

The example below copies all messages from the INBOX of your other server into
the 'OTHER-SERVER/Inbox' folder of Gmail.

::

    python imapcopy.py "imap.otherserver.com.au:993" "username:password" \
    "imap.googlemail.com:993" "username@gmail.com:password" \
    "INBOX" "OTHER-SERVER/Inbox" --verbose

Since Gmail terribly throttles uploading and downloading mails over IMAP, you 
may find the 'skip' and 'limit' options handy. If Gmail disconnected you after
copying 123 emails out of your total 1000 emails in the example shown above, 
you may use the following command to resume copying skipping the first 123 
messages.

::

    python imapcopy.py "imap.otherserver.com.au:993" "username:password" \
    "imap.googlemail.com:993" "username@gmail.com:password" \
    "INBOX" "OTHER-SERVER/Inbox" --skip 123

Similarly the 'limit' option allows you to copy only the N number of messages
excluding the skipped messages. For example, the following command will copy
message no. 124 to 223 into Gmail.

::

    python imapcopy.py "imap.otherserver.com.au:993" "username:password" \
    "imap.googlemail.com:993" "username@gmail.com:password" \
    "INBOX" "OTHER-SERVER/Inbox" --skip 123 --limit 100

Usage:

::

    usage: imapcopy.py [-h] [-q] [-v]
                   source source-auth destination destination-auth mailboxes
                   [mailboxes ...]

    positional arguments:
      source            Source host ex. imap.googlemail.com:993
      source-auth       Source host authentication ex. username@host.de:password
      destination       Destination host ex. imap.otherhoster.com:993
      destination-auth  Destination host authentication ex.
                        username@host.de:password
      mailboxes         List of mailboxes alternate between source mailbox and
                        destination mailbox.

    optional arguments:
      -h, --help        show this help message and exit
      -c, --create-mailboxes
                        Create the mailboxes on destination
      -q, --quiet       ppsssh... be quiet. (no output)
      -v, --verbose     more output please (debug level)
      -s N, --skip N    skip the first N message(s)
      -l N, --limit N   only copy N number of message(s)
  
Only tested on Python 2.7.

Oauth2 support for google
=========================

Google imap services requre oauth2 authentication. Google has provided 
Oauth2  code sample here: https://github.com/google/gmail-oauth2-tools

oauth2 authentication is taken from here.

How it works:

1. you will need Oauth client id and secret key:
   please register a project  here: https://console.developers.google.com)
   then follow to API manager, in  credentials section create Oauth client id (select: 'other' as client type)

2. instead of your password, you will need to provide your credentials in form of <yourfullemail>:appid:appsecret:



::

    python imapcopy.py "imap.gmail.com:993" "username@gmail.com:2817892479028742323.apps.googleusercontent.com:jjhJHDJKHuiJHJW" \
    "imap.otherserver.com:993" "username:password" \
    "INBOX" "OTHER-SERVER/Inbox" 

3. The script will get permission URL, which you would need to enter in your browser and obtain a verification code.
