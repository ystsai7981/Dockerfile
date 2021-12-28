FROM alpine:latest
RUN apk add neovim
WORKDIR /working
ENV HOME="/home"
RUN mkdir -p /home/.config/nvim
ADD init.vim /home/.config/nvim/
RUN chmod -R 777 /home
ENTRYPOINT ["/usr/bin/nvim"]
