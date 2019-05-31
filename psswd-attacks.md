# PASSWORD ATTACKS

All sort of password hash cracking, dictionary attacks and brute force.

## WORDLISTS

The tool `cewl` will create a custom wordlist based on a website.

Usage:

    cewl -w file.txt -d 2 -m 5 www.example.com

`-d` is the depth of links, `-m` is the minimum password length.

The tool `crunch` will create a wordlist with every possibilities with the given words.

    crunch 5 5 AB
    AAAAA
    AAAAB

would create all the possibilities made with A and B that has 5 letter length.

    crunch 7 8

This example would take forever, as it would create all imaginable combo of either 7 or 8 character length. But useful is you have an idea of the password policy or words.

## ONLINE PASSWORD ATTACKS

Need userlist and wordlist. You can use some found online but a custom made for your engagement is always a good idea. Be mindful of the language too, to include or exclude options.

### HYDRA

Hydra is a tool used to brute force against running service that requires a login.

| COMMAND                                                      | DESC                               |
|--------------------------------------------------------------|------------------------------------|
| hydra -L userlist.txt -P passwordfile.txt 192.168.2.100 pop3 | try lists against pop3 server      |
| hydra -l username                                            | specify username instead of a list |

---

## OFFLINE PASSWORD ATTACKS

Reversing the hash of a password file is much easier to avoid detection, but can be ressource hungry as you try to crack it. Since hashes are irreversible, you can guess a password, hash it and then compare to see if you have the matching hash.

### RECOVERING PSWD FROM SAM FILE IN WINDOWS

By default, the sam file is encrypted with RC4. to decrypt the bootkey (stored as SYSTEM file) do the following:

    bkhive system xpkey.txt

Then use `samdump2` to dump the hashes.

    amdump2 sam xpkey.txt

### USING JOHN THE RIPPER

By default will brute force the hash file. Useful to identify the type of hash as well. You can't brute force an NTLM hash without a wordlist.

You can add rules to `/etc/john/john.conf` to configure how it works. Example:

    rule$[0-9]$[0-9]$[0-9] # would add three numbers at the end of each word in the wordlist.


| COMMAND                                          | DESC                                    |
|--------------------------------------------------|-----------------------------------------|
| john xphashes.txt                                | basic use                               |
| john linuxhashes.txt --wordlist=passwordfile.txt | using a wordlist                        |
| john hashes.txt --rules                          | use rules as defined in the config file |

---

## MEMORY PASSWORD ATTACKS

You can use the tool `wce` to dump passwords in plaintext from an infected Windows computer by simply running the program. You need to have a user currently logged in to be able to see them.

    wce.exe -w
