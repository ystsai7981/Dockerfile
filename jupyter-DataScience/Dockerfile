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
CMD ["start-notebook.sh", "--NotebookApp.password='sha1:653d59e4b29c:320394a09d4932ed7fb4a26bda129e66a286e800'"]
