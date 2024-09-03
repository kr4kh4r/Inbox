GPG Keys || iSH>GitHub>Pass for iOS

21BDCFCEF81D828B

gpg --armor --export 21BDCFCEF81D828B
# Prints the GPG key ID, in ASCII armor format




$ gpg --export -a 21BDCFCEF81D828B > key.pub
$ gpg --export-secret-keys -a 21BDCFCEF81D828B > key