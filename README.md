# Mutt Setup

-----------------

## Installation & Setup

```bash
brew install neomutt
which neomutt && neomutt -v

or / both configs (I use both)

brew install mutt
which mutt & mutt -v 

Check your zprofile

echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile

Create folders used by mutt

mkdir -p ~/.mutt/{accounts,colors,cache/headers,cache/bodies}
touch ~/.mutt/certificates

Create your main config ~/.muttrc
mkdir ~/.muttrc

```

--------------------------

```bash

############################################
# Master mutt config
############################################
source ~/.mutt/accounts/zoho.muttrc       # account settings for your email
# I use zoho, you may use gmail, yahoo, aol, etc.
source ~/.mutt/colors/solarized-dark.muttrc  # theme (create in step 5) FYI: this feature will not work until you've set up the file with the color configs

# General UI
set sort = 'threads'
set sort_aux = 'last-date-received'
set index_format = "%4C %Z %{%b %d} %-15.15F %s"

# Caches & certs
set header_cache     = "~/.mutt/cache/headers"
set message_cachedir = "~/.mutt/cache/bodies"
set certificate_file = "~/.mutt/certificates"

# Optional: sidebar keys (toggle folder list)
set sidebar_visible = yes
set sidebar_width   = 30
bind index,pager \CP sidebar-prev
bind index,pager \CN sidebar-next
bind index,pager \CO sidebar-open

-------------------------------

Create your account email config file

code .  ~/.mutt/accounts/gmail.muttrc

code .  ~/.mutt/accounts/yahoo.muttrc

code .  ~/.mutt/accounts/aol.muttrc

code .  ~/.mutt/accounts/hotmail.muttrc

code .  ~/.mutt/accounts/zoho.muttrc

code .  ~/.mutt/accounts/outlook.muttrc

code .  ~/.mutt/accounts/comcast.muttrc



----------------------------------


############################################
# Example GMAIL Account setup 
############################################

set realname = "Test User"
set from     = "testuser@gmail.com"
set use_from = yes

# IMAP
set imap_user = "testuser@gmail.com"
set folder    = "imaps://imap.gmail.com:993"
set spoolfile = "+INBOX"
set record    = "+Sent"
set postponed = "+Drafts"
set trash     = "+Trash"

# Pull passwords from ~/.netrc
set imap_pass = `awk '/imap.gmail.com/ {print $6}' ~/.netrc`

# SMTP
set smtp_url  = "smtps://testuser@gmail.com@smtp.gmail.com:465/"
set smtp_pass = `awk '/smtp.gmail.com/ {print $6}' ~/.netrc`

# TLS
set ssl_force_tls   = yes
set ssl_starttls    = yes
set ssl_verify_host = yes
set ssl_verify_dates = yes

set move = no
set imap_keepalive = 900

----------------------------------------------

```

### Netrc Config Setup

- Create a space to store credentials (safer storage) store passwords in ~/.netrc

run:
`chmod 600 ~/.netrc`

- Netrc should contain the info below replace with your email login and app generated password

- machine imap.gmail.com login your.email@gmail.com password <APP PASSWORD>
- machine smtp.gmail.com login your.email@gmail.com password <APP PASSWORD>

------------------------------------------------

#### Enable Gmail access

- In Gmail settings → Security, enable 2FA. 2FA must be enabled!
- Generate an App Password and use that instead of your real Gmail password.

----------------------------------------------------

##### Test

- run: `mutt`

- run: `mutt`

or

- run: `neomutt`

Hit c to change folders, m to compose, q to quit.

A minimal but secure setup, for sending and receiving emails in your terminal using mutt.
[EOF]