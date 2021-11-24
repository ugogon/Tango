# Autolab - autograding docker image

FROM ubuntu:20.04
MAINTAINER TU-Berlin Computer Graphics Team <sekr@cg.tu-berlin.de>

RUN ln -fs /usr/share/zoneinfo/Europe/Berlin /etc/localtime

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
  build-essential \
  git \
  make \
  sudo \
  && rm -rf /var/lib/apt/lists/*


# Install Python
#RUN apt-get update && apt-get install -y wget
#RUN wget -qO- https://micromamba.snakepit.net/api/micromamba/linux-64/latest | tar -xvj bin/micromamba
#RUN mkdir /env
#RUN micromamba install -p /env python=3.9 c-compiler pip -c conda-forge
#SHELL ["bash", "-c"]
#RUN echo 'eval "$(micromamba shell hook -s bash)" && micromamba activate /env' >> ~/.bashrc

#RUN eval "$(micromamba shell hook -s bash)" && micromamba activate /env && pip install numpy matplotlib pillow beautifulsoup4

# RUN apt-get update  && apt-get install -y python3.9 python3.9-dev build-essential python3-pip

RUN apt-get update  && apt-get install -y python3-pip gnuplot
RUN pip3 install numpy matplotlib pillow beautifulsoup4 dill fuzzywuzzy python-Levenshtein sympy antlr4-python3-runtime==4.7.2 




# Install autodriver
WORKDIR /home
RUN useradd autolab
RUN useradd autograde
RUN mkdir autolab autograde output
RUN chown autolab:autolab autolab
RUN chown autolab:autolab output
RUN chown autograde:autograde autograde
RUN git clone --depth 1 https://github.com/autolab/Tango.git
WORKDIR Tango/autodriver
RUN make clean && make
RUN cp autodriver /usr/bin/autodriver
RUN chmod +s /usr/bin/autodriver

# Clean up
WORKDIR /home
RUN apt-get remove -y git && apt-get -y autoremove && rm -rf Tango/



# Check installation
RUN ls -l /home
RUN which autodriver
