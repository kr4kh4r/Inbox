Pass || Git Password Store

PASS

NAME

pass - stores, retrieves, generates, and synchronizes passwords securely
SYNOPSIS

pass [ COMMAND ] [ OPTIONS ]... [ ARGS ]...
DESCRIPTION

pass is a very simple password store that keeps passwords inside gpg2(1) encrypted files inside a simple directory tree residing at ˜/.password-store. The pass utility provides a series of commands for manipulating the password store, allowing the user to add, remove, edit, synchronize, generate, and manipulate passwords.
If no COMMAND is specified, COMMAND defaults to either show or ls, depending on the type of specifier in ARGS. Alternatively, if PASSWORD_STORE_ENABLE_EXTENSIONS is set to "true", and the file .extensions/COMMAND.bash exists inside the password store and is executable, then it is sourced into the environment, passing any arguments and environment variables. Extensions existing in a system-wide directory, only installable by the administrator, are always enabled.
Otherwise COMMAND must be one of the valid commands listed below.
Several of the commands below rely on or provide additional functionality if the password store directory is also a git repository. If the password store directory is a git repository, all password store modification commands will cause a corresponding git commit. Sub-directories may be separate nested git repositories, and pass will use the inner-most directory relative to the current password. See the EXTENDED GIT EXAMPLE section for a detailed description using init and git(1).
The init command must be run before other commands in order to initialize the password store with the correct gpg key id. Passwords are encrypted using the gpg key set with init.
There is a corresponding bash completion script for use with tab completing password names in bash(1).
COMMANDS

init [ --path=sub-folder, -p sub-folder ] gpg-id...
Initialize new password storage and use gpg-id for encryption. Multiple gpg-ids may be specified, in order to encrypt each password with multiple ids. This command must be run first before a password store can be used. If the specified gpg-id is different from the key used in any existing files, these files will be reencrypted to use the new id. Note that use of gpg-agent(1) is recommended so that the batch decryption does not require as much user intervention. If --path or -p is specified, along with an argument, a specific gpg-id or set of gpg-ids is assigned for that specific sub folder of the password store. If only one gpg-id is given, and it is an empty string, then the current .gpg-id file for the specified sub-folder (or root if unspecified) is removed.
ls subfolder
List names of passwords inside the tree at subfolder by using the tree(1) program. This command is alternatively named list.
grep [GREPOPTIONS] search-string
Searches inside each decrypted password file for search-string, and displays line containing matched string along with filename. Uses grep(1) for matching. GREPOPTIONS are passed to grep(1) as-is. (Note: the GREP_OPTIONS environment variable functions as well.)
find pass-names...
List names of passwords inside the tree that match pass-names by using the tree(1) program. This command is alternatively named search.
show [ --clip[=line-number], -c[line-number] ] [ 
--qrcode[=line-number], -q[line-number] ] pass-name
Decrypt and print a password named pass-name. If --clip or -c is specified, do not print the password but instead copy the first (or otherwise specified) line to the clipboard using xclip(1) or wl-clipboard(1) and then restore the clipboard after 45 (or PASSWORD_STORE_CLIP_TIME) seconds. If --qrcode or -q is specified, do not print the password but instead display a QR code using qrencode(1) either to the terminal or graphically if supported.
insert [ --echo, -e | --multiline, -m ] [ --force, -f ] pass-name
Insert a new password into the password store called pass-name. This will read the new password from standard in. If --echo or -e is not specified, disable keyboard echo when the password is entered and confirm the password by asking for it twice. If --multiline or -m is specified, lines will be read until EOF or Ctrl+D is reached. Otherwise, only a single line from standard in is read. Prompt before overwriting an existing password, unless --force or -f is specified. This command is alternatively named add.
edit pass-name
Insert a new password or edit an existing password using the default text editor specified by the environment variable EDITOR or using vi(1) as a fallback. This mode makes use of temporary files for editing, but care is taken to ensure that temporary files are created in /dev/shm in order to avoid writing to difficult-to-erase disk sectors. If /dev/shm is not accessible, fallback to the ordinary TMPDIR location, and print a warning.
generate [ --no-symbols, -n ] [ --clip, -c ] [ --in-place, -i | 
--force, -f ] pass-name [pass-length]
Generate a new password using /dev/urandom of length pass-length (or PASSWORD_STORE_GENERATED_LENGTH if unspecified) and insert into pass-name. If --no-symbols or -n is specified, do not use any non-alphanumeric characters in the generated password. The character sets used in generating passwords can be changed with the PASSWORD_STORE_CHARACTER_SET and PASSWORD_STORE_CHARACTER_SET_NO_SYMBOLS environment variables, described below. If --clip or -c is specified, do not print the password but instead copy it to the clipboard using xclip(1) or wl-clipboard(1) and then restore the clipboard after 45 (or PASSWORD_STORE_CLIP_TIME) seconds. If --qrcode or -q is specified, do not print the password but instead display a QR code using qrencode(1) either to the terminal or graphically if supported. Prompt before overwriting an existing password, unless --force or -f is specified. If --in-place or -i is specified, do not interactively prompt, and only replace the first line of the password file with the new generated password, keeping the remainder of the file intact.
rm [ --recursive, -r ] [ --force, -f ] pass-name
Remove the password named pass-name from the password store. This command is alternatively named remove or delete. If --recursive or -r is specified, delete pass-name recursively if it is a directory. If --force or -f is specified, do not interactively prompt before removal.
mv [ --force, -f ] old-path new-path
Renames the password or directory named old-path to new-path. This command is alternatively named rename. If --force is specified, silently overwrite new-path if it exists. If new-path ends in a trailing /, it is always treated as a directory. Passwords are selectively reencrypted to the corresponding keys of their new destination.
cp [ --force, -f ] old-path new-path
Copies the password or directory named old-path to new-path. This command is alternatively named copy. If --force is specified, silently overwrite new-path if it exists. If new-path ends in a trailing /, it is always treated as a directory. Passwords are selectively reencrypted to the corresponding keys of their new destination.
git git-command-args...
If the password store is a git repository, pass git-command-args as arguments to git(1) using the password store as the git repository. If git-command-args is init, in addition to initializing the git repository, add the current contents of the password store to the repository in an initial commit. If the git config key pass.signcommits is set to true, then all commits will be signed using user.signingkey or the default git signing key. This config key may be turned on using: ‘pass git config --bool --add pass.signcommits true‘
help
Show usage message.
version
Show version information.
SIMPLE EXAMPLES

Initialize password store
zx2c4@laptop ˜ $ pass init Jason@zx2c4.com 
mkdir: created directory ‘/home/zx2c4/.password-store’ 
Password store initialized for Jason@zx2c4.com.
List existing passwords in store
zx2c4@laptop ˜ $ pass 
Password Store 
├── Business 
│ ├── some-silly-business-site.com 
│ └── another-business-site.net 
├── Email 
│ ├── donenfeld.com 
│ └── zx2c4.com 
└── France 
├── bank 
├── freebox 
└── mobilephone
Alternatively, "pass ls".
Find existing passwords in store that match .com
zx2c4@laptop ˜ $ pass find .com 
Search Terms: .com 
├── Business 
│ ├── some-silly-business-site.com 
└── Email 
├── donenfeld.com 
└── zx2c4.com
Alternatively, "pass search .com".
Show existing password
zx2c4@laptop ˜ $ pass Email/zx2c4.com 
sup3rh4x3rizmynam3
Copy existing password to clipboard
zx2c4@laptop ˜ $ pass -c Email/zx2c4.com 
Copied Email/jason@zx2c4.com to clipboard. Will clear in 45 seconds.
Add password to store
zx2c4@laptop ˜ $ pass insert Business/cheese-whiz-factory 
Enter password for Business/cheese-whiz-factory: omg so much cheese what am i gonna do
Add multiline password to store
zx2c4@laptop ˜ $ pass insert -m Business/cheese-whiz-factory 
Enter contents of Business/cheese-whiz-factory and press Ctrl+D when finished:
Hey this is my 
awesome 
multi 
line 
passworrrrrrrrd. 
ˆD
Generate new password
zx2c4@laptop ˜ $ pass generate Email/jasondonenfeld.com 15 
The generated password to Email/jasondonenfeld.com is: 
$(-QF&Q=IN2nFBx
Generate new alphanumeric password
zx2c4@laptop ˜ $ pass generate -n Email/jasondonenfeld.com 12 
The generated password to Email/jasondonenfeld.com is: 
YqFsMkBeO6di
Generate new password and copy it to the clipboard
zx2c4@laptop ˜ $ pass generate -c Email/jasondonenfeld.com 19 
Copied Email/jasondonenfeld.com to clipboard. Will clear in 45 seconds.
Remove password from store
zx2c4@laptop ˜ $ pass remove Business/cheese-whiz-factory 
rm: remove regular file ‘/home/zx2c4/.password-store/Business/cheese-whiz-factory.gpg’? y 
removed ‘/home/zx2c4/.password-store/Business/cheese-whiz-factory.gpg’
EXTENDED GIT EXAMPLE

Here, we initialize new password store, create a git repository, and then manipulate and sync passwords. Make note of the arguments to the first call of pass git push; consult git-push(1) for more information.
zx2c4@laptop ˜ $ pass init Jason@zx2c4.com 
mkdir: created directory ‘/home/zx2c4/.password-store’ 
Password store initialized for Jason@zx2c4.com.
zx2c4@laptop ˜ $ pass git init 
Initialized empty Git repository in /home/zx2c4/.password-store/.git/ 
[master (root-commit) 998c8fd] Added current contents of password store. 
1 file changed, 1 insertion(+) 
create mode 100644 .gpg-id
zx2c4@laptop ˜ $ pass git remote add origin kexec.com:pass-store
zx2c4@laptop ˜ $ pass generate Amazon/amazonemail@email.com 21 
mkdir: created directory ‘/home/zx2c4/.password-store/Amazon’ 
[master 30fdc1e] Added generated password for Amazon/amazonemail@email.com to store. 
1 file changed, 0 insertions(+), 0 deletions(-) 
create mode 100644 Amazon/amazonemail@email.com.gpg 
The generated password to Amazon/amazonemail@email.com is: 
<5m,_BrZY‘antNDxKN<0A
zx2c4@laptop ˜ $ pass git push -u --all 
Counting objects: 4, done. 
Delta compression using up to 2 threads. 
Compressing objects: 100% (3/3), done. 
Writing objects: 100% (4/4), 921 bytes, done. 
Total 4 (delta 0), reused 0 (delta 0) 
To kexec.com:pass-store 
* [new branch] master -> master 
Branch master set up to track remote branch master from origin.
zx2c4@laptop ˜ $ pass insert Amazon/otheraccount@email.com 
Enter password for Amazon/otheraccount@email.com: som3r3a11yb1gp4ssw0rd!!88** 
[master b9b6746] Added given password for Amazon/otheraccount@email.com to store. 
1 file changed, 0 insertions(+), 0 deletions(-) 
create mode 100644 Amazon/otheraccount@email.com.gpg
zx2c4@laptop ˜ $ pass rm Amazon/amazonemail@email.com 
rm: remove regular file ‘/home/zx2c4/.password-store/Amazon/amazonemail@email.com.gpg’? y 
removed ‘/home/zx2c4/.password-store/Amazon/amazonemail@email.com.gpg’ 
rm ’Amazon/amazonemail@email.com.gpg’ 
[master 288b379] Removed Amazon/amazonemail@email.com from store. 
1 file changed, 0 insertions(+), 0 deletions(-) 
delete mode 100644 Amazon/amazonemail@email.com.gpg
zx2c4@laptop ˜ $ pass git push 
Counting objects: 9, done. 
Delta compression using up to 2 threads. 
Compressing objects: 100% (5/5), done. 
Writing objects: 100% (7/7), 1.25 KiB, done. 
Total 7 (delta 0), reused 0 (delta 0) 
To kexec.com:pass-store
FILES

˜/.password-store
The default password storage directory.
˜/.password-store/.gpg-id
Contains the default gpg key identification used for encryption and decryption. Multiple gpg keys may be specified in this file, one per line. If this file exists in any sub directories, passwords inside those sub directories are encrypted using those keys. This should be set using the init command.
˜/.password-store/.extensions
The directory containing extension files.
ENVIRONMENT VARIABLES

PASSWORD_STORE_DIR
Overrides the default password storage directory.
PASSWORD_STORE_KEY
Overrides the default gpg key identification set by init. Keys must not contain spaces and thus use of the hexadecimal key signature is recommended. Multiple keys may be specified separated by spaces.
PASSWORD_STORE_GPG_OPTS
Additional options to be passed to all invocations of GPG.
PASSWORD_STORE_X_SELECTION
Overrides the selection passed to xclip, by default clipboard. See xclip(1) for more info.
PASSWORD_STORE_CLIP_TIME
Specifies the number of seconds to wait before restoring the clipboard, by default 45 seconds.
PASSWORD_STORE_UMASK
Sets the umask of all files modified by pass, by default 077.
PASSWORD_STORE_GENERATED_LENGTH
The default password length if the pass-length parameter to generate is unspecified.
PASSWORD_STORE_CHARACTER_SET
The character set to be used in password generation for generate. This value is to be interpreted by tr. See tr(1) for more info.
PASSWORD_STORE_CHARACTER_SET_NO_SYMBOLS
The character set to be used in no-symbol password generation for generate, when --no-symbols, -n is specified. This value is to be interpreted by tr. See tr(1) for more info.
PASSWORD_STORE_ENABLE_EXTENSIONS
This environment variable must be set to "true" for extensions to be enabled.
PASSWORD_STORE_EXTENSIONS_DIR
The location to look for executable extension files, by default PASSWORD_STORE_DIR/.extensions.
PASSWORD_STORE_SIGNING_KEY
If this environment variable is set, then all .gpg-id files and non-system extension files must be signed using a detached signature using the GPG key specified by the full 40 character upper-case fingerprint in this variable. If multiple fingerprints are specified, each separated by a whitespace character, then signatures must match at least one. The init command will keep signatures of .gpg-id files up to date.
EDITOR
The location of the text editor used by edit.
SEE ALSO

gpg2(1), tr(1), git(1), xclip(1), wl-clipboard(1), qrencode(1).