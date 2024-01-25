# GIT

All things related to using git


## Using Git on NeSI:
You now have an ssh key set up so this should be very straightforward.

    git init

    git remote add origin git@github.com:natforsdick/repo-name.git

Then add and commit at least one file before doing the next steps.
    
    git branch -m master main

    git status # See what files are tracked, modified etc.

    git diff --color-words # View modifications

    git add <file>

    git commit -am "message"

    git push origin main

## Added files/directories that you no longer want git to track?

Using -n makes it a dry run so you can check what you are removing.

    git rm -r --cached <file/dir> -n

## .gitignore

To add items to .gitignore
    
    echo '*.r' >> .gitignore

You can have .gitignores in each directory within a git repo, or you can have a single one in the top level directory.

## Error messages

1. When pushing to github: 
    error: src refspec master does not match any. 
This error most likely means your branch name is incorrect. You can reset the branch name as in the 'Using Git on NeSI' section, then try to push again.

If Git is hanging in VS Code/Linux generally, it's likely an ssh issue. First, check that your `~/.ssh/config` file ssh IDs match the key filenames. Then check that the `~/.ssh` directory has chmod 700 permissions (-rwx------). Then make sure that the config file has chmod 600 permissions (drwx------). Now test authentication with `ssh -Tv git@github.com`. 

## Changing repo url

If you ever change the name of your repo, this will change the url. While git will still know where to push to, you are best to reset the url:

    git remote set-url origin git@github.com:natforsdick/new-repo-name.git

## Create Personal Access Token on Github

From August 13, 2021, Github is no longer accepting account passwords when authenticating Git operations. You need to add PAT (Personal Access Token) instead, you can follow the below method to add PFA on your system

From your Github account, go to Settings => Developer Settings => Personal Access Token => Generate New Token (Give your password) => Fillup the form => click Generate token => Copy the generated Token, it will be something like ghp_sFhFsSHhTzMDreGRLjmks4Tzuzgthdvfsrta

Now follow below method based on your machine:

### For MAC OS

Click on the Spotlight icon (magnifying glass) on the right side of the menu bar. Type Keychain access then press the Enter key to launch the app => In Keychain Access, search for github.com => Find the internet password entry for github.com => Edit or delete the entry accordingly => You are done

### For Linux based OS

For Linux, You need to configure the local GIT client with a username and email address,

    git config --global user.name ""
    git config --global user.email ""
    git config -l

Once GIT is configured, we can begin using it to access GitHub. Example :

    git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
    > Cloning into `Spoon-Knife`...
    Username for 'https://github.com' : username
    Password for 'https://github.com' : give your personal access token here

Now cache the given record in your computer to remembers the token :

    git config --global credential.helper cache

If needed, anytime you can delete the cache record by :

    git config --global --unset credential.helper



## Using GitHub with SSH

First generate a new SSH key (email is your GitHub email) - make sure to set the path or name of the new key, and add a passphrase:

   ssh-keygen -t ed25519 -C "your_email@example.com"

Start your SSH agent

    eval "$(ssh-agent -s)"


Suppose you have a key pair specifically to access GitHub, and it is at ~/.ssh/github_key (private key) and ~/.ssh/github_key.pub (public key). 


You can create an entry in ~/.ssh/config as follows: 

Host github 
	HostName github.com
	User git
	AddKeysToAgent yes
	UseKeychain yes
	IdentityFile ~/.ssh/github_key 

Then to add your private key to the ssh-agent:

    ssh-add ~/.ssh/id_ed25519

Copy your public key, and add it to your GitHub account Settings > SSH & GPG keys.

Then to confirm that everything is working correctly:

    ssh -vT git@github.com

You should get a message that you've successfully authenticated. 

With this in place, your remote repository URLs that are on github.com should start with: 
ssh://github/ 
And you should be able to use git@github.com:natforsdick/repo.git from hereon when pushing/pulling.

And both Git and SSH will from then on select the correct key pair automatically when trying to access that repo. But putting ssh://github/ in place must be done on a remote-repo-by-remote-repo basis, which means, for each of your local repositories, updating all the remote repositories known to that repo. 
