FROM ubuntu:18.04

RUN apt-get update && \
	apt-get install curl git htop vim wget openjdk-8-jdk python3-pip -y && \
	apt-get autoclean  -y && \
	apt-get autoremove -y 

# nodejs 10
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
	apt-get install -y nodejs

WORKDIR /jupyter/data/

# building the repo
RUN git clone https://github.com/matheusmota/facens-dataviz
RUN pip3 install -r facens-dataviz/binder/requirements.txt
RUN mkdir conda-bld
RUN sh facens-dataviz/binder/postBuild

ENV LANG=C.UTF-8

EXPOSE 8888

RUN rm conda-bld -R

CMD jupyter-lab --ip=0.0.0.0 --port=8888 --no-browser --notebook-dir=/jupyter/data --allow-root --NotebookApp.token=''