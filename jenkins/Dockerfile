FROM jenkins/jenkins:lts
 
USER root
RUN apt-get update && apt-get install -y sudo && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

USER jenkins

COPY "MoneyWise - Unit Test (Previously responsible of all MoneyWiseCICD)/config.xml" "/usr/share/jenkins/MoneyWise - Unit Test (Previously responsible of all MoneyWiseCICD)/config.xml"
COPY "MoneyWise - BDD Tests/config.xml" "/usr/share/jenkins/MoneyWise - BDD Tests/config.xml"
COPY "MoneyWise - Deploy/config.xml" "/usr/share/jenkins/MoneyWise - Deploy/config.xml"
COPY "MoneyWise - Health Check/config.xml" "/usr/share/jenkins/MoneyWise - Health Check/config.xml"
COPY "MoneyWise - Cleanup/config.xml" "/usr/share/jenkins/MoneyWise - Cleanup/config.xml"
COPY plugins.txt /usr/share/jenkins/plugins.txt
COPY backend-variables.env /usr/share/jenkins/backend-variables.env
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN sudo apt update
RUN sudo curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh
RUN sudo bash nodesource_setup.sh
RUN sudo apt-get install -y nodejs
RUN sudo apt install -y yarn
RUN sudo apt install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev docker-compose wget
RUN sudo curl -O https://www.python.org/ftp/python/3.8.6/Python-3.8.6.tar.xz
RUN sudo tar -xf Python-3.8.6.tar.xz
RUN cd Python-3.8.6 && sudo ./configure --enable-optimizations --enable-loadable-sqlite-extensions
RUN cd Python-3.8.6 && sudo make
RUN cd Python-3.8.6 && sudo make altinstall
RUN sudo curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN sudo python3.8 get-pip.py
RUN /usr/local/bin/install-plugins.sh $(cat /usr/share/jenkins/plugins.txt)
RUN sudo rm -rf Python-3.8.6*




