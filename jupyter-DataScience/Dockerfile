FROM jupyter/datascience-notebook
ENV NB_USER=ystsai
ENV NB_UID=1000
ENV NB_GID=1000
ENV CHOWN_HOME=yes
ENV GRANT_SUDO=yes
ENV JUPYTER_ENABLE_LAB=yes
ENV RESTARTABLE=yes
WORKDIR /home/ystsai/work
USER root
RUN apt-get update && apt-get install -y \
ssh && \
echo "ystsai:\$1\$4jqlyaXh\$qNbImBVBG5U97ndP9P.Bs/" | chpasswd && \
echo "Port 22" >> /etc/ssh/sshd_config && \
echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config && \
echo "PermitRootLogin yes" >> /etc/ssh/sshd_config && \
echo "X11Forwarding yes" >> /etc/ssh/sshd_config && \
echo "X11DisplayOffset 10" >> /etc/ssh/sshd_config && \
echo "X11UseLocalhost no" >> /etc/ssh/sshd_config && \
rm -rf /var/lib/apt/lists/*
EXPOSE 22
CMD ["start-notebook.sh", "--NotebookApp.password='sha1:653d59e4b29c:320394a09d4932ed7fb4a26bda129e66a286e800'"]
