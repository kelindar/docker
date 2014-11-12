FROM misakai/ubuntu
MAINTAINER Roman Atachiants "roman@misakai.com"

# Add Oracle JRE 7 installer package repository to apt sources:

# 1 way (which pulls in a ton of stuff on our minimal system):
# RUN apt-get -y install software-properties-common
# RUN add-apt-repository ppa:webupd8team/java

# Another way (much simpler, doesn't require any installations):
# RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list
# RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list
# RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886

# However you add the sources, great. Then install the Oracle JRE 7 installer:
# RUN apt-get -y update
# RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
# RUN apt-get -y install oracle-java7-installer


# Or maybe just use OpenJDK JRE for now:
RUN apt-get -y install openjdk-7-jre-headless --no-install-recommends --no-install-suggests

# Curses, the JDK installation is pulling in a sound library and x11 :(
# RUN apt-get -y install openjdk-7-jdk --no-install-recommends --no-install-suggests