FROM nvcr.io/nvidia/pytorch:22.03-py3
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
sudo \
&& rm -rf /var/lib/apt/lists/*

ENV YOURNAME=ystsai
RUN groupadd -g 1000 ${YOURNAME} \
&& useradd -m -u 1000 -g 1000 -G sudo,root ${YOURNAME} \
&& echo "${YOURNAME}:\$1\$4jqlyaXh\$qNbImBVBG5U97ndP9P.Bs/" | chpasswd -e

RUN python -m pip install --upgrade pip \
&& pip install --upgrade jupyterlab pandas scikit-learn \
&& pip install tqdm ipywidgets timm

ADD deepcat.sh /root
RUN cat /root/deepcat.sh > /home/${YOURNAME}/.bashrc \
&& cat /root/.bashrc >> /home/${YOURNAME}/.bashrc

ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

USER ${YOURNAME}

RUN jupyter lab --generate-config \
&& echo "c.ServerApp.password = 'argon2:\$argon2id\$v=19\$m=10240,t=10,p=8\$Utr2gKVeHPNUponhvQYduw\$O47MwC/QqmHDwKg8mW1nCjCPwtnS+NmYOHpdjP60tW8'" >> /home/${YOURNAME}/.jupyter/jupyter_lab_config.py

WORKDIR /home/${YOURNAME}/work
EXPOSE 8888 22 5900 6006
ENTRYPOINT ["/tini", "--"]
CMD ["jupyter", "lab", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
