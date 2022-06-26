# Build a development environment using Docker Desktop.

## Advantages
1. Reduce the time it takes to build a development environment.<br>
2. Can ensure that they are in the same environment.<br>
3. No need to change the local environment.

## Disadvantage
1. Cost of learning about Docker.<br>
2. Requires a certain amount of machine power.<br>

## Goals for this time
Run and debug Python without installing a local Python environment.<br>

### Preparation of the environment
#### 1) Installing Windows Subsystem for Linux.<br>

-Check for situations where the "Windows Subsystem for Linux" is not enabled.<br>
![wsl_ini](./picture/wsl_ini.JPG)<br>

1-1) Run PowerShell as an administrator and execute the following commands.<br>
wsl --install<br>
<br>
1-2) After Ubuntu starts, set a username and password.<br>
Note 1: If you run wsl --install and see WSL help text, run wsl --list --online to list available distributions, then run wsl --install -d DistroName to Install.<br>
Note 2: Passwords are not displayed.<br>
<br>
-Confirm that the "Windows Subsystem for Linux" is enabled.<br>
![wsl_aft](./picture/wsl_aft.JPG)

Execute the following command in PowerShell to check the version of wsl, and if VERSION is 1, execute 1-3) or later.<br>
wsl -l -v<br>
<br>
1-3) Download the Linux kernel update package.<br>
https://docs.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package<br>
<br>
1-4) Run PowerShell as an administrator and execute the following commands.<br>
wsl --set-version distro_name 2<br>
Example.wsl --set-version Ubuntu 2<br>

Then check the version.<br>
![wsl2](./picture/wsl2.JPG) <br>
<br>

#### 2) Install Windows Terminal (optional)
Refer to the following sites.<br>
https://docs.microsoft.com/en-us/windows/terminal/install<br>
<br>

#### 3) Deploy Docker desktop with WSL 2<br>
3-1) Download and run the installer from the following site.<br>
https://docs.docker.com/desktop/windows/wsl/<br>
<br>
3-2) Make sure the two checkboxes are checked, click OK, and run the installation.<br>
![docker_desktop](./picture/docker_desktop.JPG)<br>
<br>
3-3) If a task called Vmmem ever takes up a lot of memory, limit the memory by putting the following in C:\Users\[username]\.wslconfig.<br>
<br>
[wsl2]<br>
memory=1GB<br>
<br>
Then, run PowerShell as an administrator and reboot with the following command.<br>
Get-Service LxssManager | Restart-Service<br>
<br>

#### 4) Introducing Visual Studio Code<br>
Refer to the following sites.<br>
https://code.visualstudio.com/
<br>

#### 5) Introduction of Remote-Containers (Visual Studio Code extension)<br>
Search for Remote-Containers in the Extensions section for information on installing extensions.<br>
<br>

### Sample Summary Description
- Code Reference
https://dev.classmethod.jp/articles/vscode-container-connect/
- Link to sample created
https://github.com/ShugoYoko/docker_dev.git<br>
- Key points of docker-compose.yml<br>
volumes:
      - ./src:/home/:cached<br>
The src folder can be mounted to home in the Docker container to reflect changes in the source.
- Key points of .devcontainer/devcontainer.json<br>
 "extensions": [
      "ms-python.python"
  ]<br>
Extensions required for debugging are installed in containers.
<br>

### Verification method using samples<br>
#### 1) Start Docker Desktop<br>

#### 2) If git is installed, run the following command.<br>
git clone https://github.com/ShugoYoko/docker_dev.git<br>

#### 3) Open docker_dev folder in Visual studio code<br>

#### 4) Reopen in Container to start container.<br>
Initially, it takes time to create the container.
![reopen](./picture/reopen.JPG)<br>

#### 5) Open New Terminal from Visual Studio Code Terminal and execute the command to confirm that Python is installed and test.py can be executed.

![python](./picture/python.JPG)<br>

#### 6) Debugging can be performed by setting breakpoints.

![breakpoint](./picture/breakpoint.JPG)<br>

![setting](./picture/setting.JPG)<br>

![breakpoint](./picture/breakpoint.JPG)<br>

![debug](./picture/debug.JPG)<br>

Select "Reopen Folder Locally" to return.
![local](./picture/local.JPG)<br>

## Summary
This method is also effective when it is necessary to prepare a database or to develop a web application that includes a database. I would like to continue to examine various types in the future.<br>

























