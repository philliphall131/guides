# Windows Computer Setup

## These are the downloads and setup tasks to get a windows computer to development ready

1) Installations:
    - Slack
    - Zoom
    - VS Code
    - Python

2) Windows Terminal Setup
    - https://docs.microsoft.com/en-us/windows/terminal/install

3) WSL Setup
    - https://docs.microsoft.com/en-us/windows/wsl/install
    - After installation, restart computer, setup a user then:
    (https://docs.microsoft.com/en-us/windows/wsl/setup/environment)
~~~
sudo apt update && sudo apt upgrade
~~~

4) VS Code Remote
    - Open a remote VS Code into WSL, load in any extensions on the "VM" side that arent carried over. There is a note in extensions about which ones are active in remote or not

5) Git, Github, and Git Credential Manager Setup
    - Install git on Windows: https://git-scm.com/download/win
    - Initialize Git Credential Manager by push/pulling something from github (will trigger interactive gh setup)
    - Install git on WSL
~~~
sudo apt-get install git
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"
git config --global credential.helper "/mnt/c/Program\ Files\ \(x86\)/Git/mingw64/bin/git-credential-manager-core.exe"
~~~

5) NPM/N/Node
~~~
sudo apt-get install npm
sudo npm install -g n
sudo n stable
~~~

6) Bash Profiles


