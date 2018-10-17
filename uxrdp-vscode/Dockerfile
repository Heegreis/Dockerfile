
FROM danielguerra/ubuntu-xrdp:16.04

# https://code.visualstudio.com/docs/setup/linux
RUN apt-get update
RUN apt-get -y install wget
RUN wget -O code.deb https://go.microsoft.com/fwlink/?LinkID=760868
RUN apt-get -y install libnotify4
RUN apt-get -y install libnss3
RUN apt-get -y install libxkbfile1
RUN apt-get -y install libgconf-2-4
RUN apt-get -y install libsecret-1-0
RUN apt-get -y install gnupg
RUN dpkg -i code.deb
RUN apt-get install -f
RUN apt-get -y install libproj-dev
RUN apt-get -y install curl
RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
RUN apt-get -y install apt-transport-https
RUN apt-get update
RUN apt-get -y install code
RUN apt-get -y install libxss1
RUN apt-get -y install libasound2
RUN apt-get -y install libx11-xcb1
RUN code --user-data-dir="/home/.vscode-root"
