# Windows Computer Setup

## These are the downloads and setup tasks to get a windows computer to development ready

1) Installations:
    - Slack
    - Zoom
    - VS Code
    - Python

2) WSL Setup
    - https://docs.microsoft.com/en-us/windows/wsl/install
    - VS Code: Install necessary remote extensions on WSL side 
    - After installation, restart computer, setup a user then:
~~~
sudo apt update && sudo apt upgrade
~~~

3) Windows Terminal Setup
    - https://docs.microsoft.com/en-us/windows/terminal/install

4) Git, Github, and Git Credential Manager Setup
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


