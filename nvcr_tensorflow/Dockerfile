FROM nvcr.io/nvidia/tensorflow:22.01-tf2-py3
EXPOSE 8888 22 5900 6006
RUN apt-get update && \
apt-get install -y sudo \
python3-opencv \
nodejs \
npm && \
rm -rf /var/lib/apt/lists/*
RUN mkdir -p /home/ystsai/work && \
groupadd -g 1000 ystsai && \
useradd -d /home/ystsai -u 1000 -g 1000 -G sudo ystsai && \
echo "ystsai:\$1\$4jqlyaXh\$qNbImBVBG5U97ndP9P.Bs/" | chpasswd -e
WORKDIR /home/ystsai/work

RUN python -m pip install --upgrade pip && \
pip install lxml jupyterlab-lsp && \
pip install 'python-lsp-server[all]' && \
pip install --upgrade jupyterlab pandas scikit-learn tensorboard tensorflow-addons && \
pip install -q "tqdm>=4.36.1" && \
pip install ipywidgets

ADD deepcat.sh /root
RUN cat /root/deepcat.sh > /home/ystsai/.bashrc && \
cat /root/.bashrc >> /home/ystsai/.bashrc && \
chown -R ystsai:ystsai /home/ystsai && \
chown -R ystsai:ystsai /usr/local/share/jupyter

ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

USER ystsai

RUN jupyter lab --generate-config && \
echo "c.ServerApp.password = 'argon2:\$argon2id\$v=19\$m=10240,t=10,p=8\$Utr2gKVeHPNUponhvQYduw\$O47MwC/QqmHDwKg8mW1nCjCPwtnS+NmYOHpdjP60tW8'" >> /home/ystsai/.jupyter/jupyter_lab_config.py

ENTRYPOINT ["/tini", "--"]
CMD ["jupyter", "lab", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
