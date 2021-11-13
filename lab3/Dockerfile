FROM brunneis/python:3.8.6-ubuntu-20.04

RUN apt-get update && apt-get install -y python3-setuptools 

# wget gnupg2 software-properties-common
# RUN wget -O my_sth http://download.sgjp.pl/apt/sgjp.gpg.key | apt-key add my_sth
# RUN apt-add-repository http://download.sgjp.pl/apt/ubuntu
# RUN apt-get update && apt-get install -y python3-morfeusz2


WORKDIR /app

COPY requirements.txt .
COPY ustawy.tar.gz .
COPY lab3.ipynb .



RUN pip3 install -r requirements.txt
RUN pip3 install morfeusz2

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
