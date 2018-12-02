FROM ubuntu:16.04
EXPOSE 3000

RUN apt-get update && apt-get install -y git curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
RUN git clone https://github.com/rovaniemi/exam-archive-prototype

WORKDIR /exam-archive-prototype
RUN npm install
CMD npm start