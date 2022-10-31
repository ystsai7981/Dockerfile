FROM nvcr.io/nvidia/pytorch:22.03-py3
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
sudo \
&& rm -rf /var/lib/apt/lists/*

ENV YOURNAME=deepcat
RUN groupadd -g 1000 ${YOURNAME} \
&& useradd -m -u 1000 -g 1000 -G sudo,root ${YOURNAME} \
&& echo "${YOURNAME}:deepcat" | chpasswd

RUN python -m pip install --upgrade pip jupyterlab\
&& pip install jupyterlab-lsp 'python-lsp-server[all]'

ADD deepcat.sh /root
RUN cat /root/deepcat.sh > /home/${YOURNAME}/.bashrc \
&& cat /root/.bashrc >> /home/${YOURNAME}/.bashrc

ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

USER ${YOURNAME}

RUN jupyter lab --generate-config \
&& echo "c.ServerApp.password = 'argon2:\$argon2id\$v=19\$m=10240,t=10,p=8\$edtPKRZRaQfmpDoAVtqTwQ\$H9AuuTvbSuQKQbLV+ZGRJFdsAIKnG7bXmlViCVJ2ZUk'" >> /home/${YOURNAME}/.jupyter/jupyter_lab_config.py

WORKDIR /workspace
EXPOSE 8888
ENTRYPOINT ["/tini", "--"]
CMD ["jupyter", "lab", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
