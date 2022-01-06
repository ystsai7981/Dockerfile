FROM nvcr.io/nvidia/pytorch:21.11-py3
RUN apt-get update && \
apt-get install -y sudo && \
rm -rf /var/lib/apt/lists/*
RUN mkdir -p /home/ystsai/work && \
groupadd -g 1000 ystsai && \
useradd -d /home/ystsai -u 1000 -g 1000 -G sudo ystsai && \
echo "ystsai:\$1\$4jqlyaXh\$qNbImBVBG5U97ndP9P.Bs/" | chpasswd -e
WORKDIR /home/ystsai/work

RUN jupyter lab --generate-config && \
echo "c.LabApp.password = 'argon2:\$argon2id\$v=19\$m=10240,t=10,p=8\$Utr2gKVeHPNUponhvQYduw\$O47MwC/QqmHDwKg8mW1nCjCPwtnS+NmYOHpdjP60tW8'" >> /root/.jupyter/jupyter_notebook_config.py && \
cp -r /root/.jupyter /home/ystsai
ADD deepcat.sh /root
RUN cat /root/deepcat.sh > /home/ystsai/.bashrc && \
cat /root/.bashrc >> /home/ystsai/.bashrc && \
chown -R ystsai:ystsai /home/ystsai && \
chmod -R 777 /home/ystsai

ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

EXPOSE 8888
CMD ["jupyter", "lab", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
