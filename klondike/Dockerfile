FROM misakai/ubuntu
MAINTAINER Roman Atachiants <roman@misakai.com>

# Install dependencies
RUN apt-get update -q -y && \
    apt-get dist-upgrade -q -y && \
    apt-get install -q -y \
    	mono-xsp2 \
    	mono-xsp2-base \
    	unzip

# Setup lbManager runit service
RUN mkdir -p /etc/service/lbManager
ADD https://github.com/themotleyfool/Klondike/releases/download/v1.6.2/Klondike-Release-1.6.2.zip /tmp/
RUN unzip /tmp/Klondike-Release-1.6.2.zip
RUN mv /tmp/Klondike-Release-1.6.2 /tmp/klondike
