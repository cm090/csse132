# Saving your Rose credentials
By default, your local git repository will not save your account password. Every time you want to work with the remote branch, you will be prompted to authenticate. To prevent this problem, there is a simple way to securely store your password.

Begin by navigating to the source folder of your local repository.
```
cd /path/to/2122b-csse132-<username>
```
Replace `<username>` with your Rose username

Generate a new keygen file for your pi. This will locally store and encrypt passwords.
```
ssh-keygen
```

Press enter a few times until you see a square with various symbols. You do not have to enter a passphrase. The square is the randomart image that represents encryption. Continue by storing the SSH password for your remote repository.
```
ssh-copy-id -i ~/.ssh/id_rsa <username>@gitter.csse.rose-hulman.edu
```
Replace `<username>` with your rose username.

You will then be prompted for your Rose password. Type it in (keystrokes are not represented in the terminal) and press enter.

That's it! Test your keyfile by performing an action with the remote repository.
```
git pull
```

You should not be prompted to enter your password.
