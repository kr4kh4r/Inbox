ssh info || ssh-keygen

~/.ssh/id_rsa
Contains the protocol version 2 RSA authentication identity of the user. This file should not be readable by anyone but the user. It is possible to specify a passphrase when generating the key; that passphrase will be used to encrypt the private part of this file using 3DES. This file is not automatically accessed by ssh-keygen but it is offered as the default file for the private key. ssh(1) will read this file when a login attempt is made.

~/.ssh/id_rsa.pub
Contains the protocol version 2 RSA public key for authentication. The contents of this file should be added to ~/.ssh/authorized_keys on all machines where the user wishes to log in using public key authentication. There is no need to keep the contents of this file secret.

#ssh
#cmd 