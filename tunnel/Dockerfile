FROM ubuntu:24.04

#必須パッケージのインストール
RUN apt-get update && \
    apt-get -y install wget unzip curl

#Cloudflare Access
RUN mkdir -p --mode=0755 /usr/share/keyrings && \
    curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg | tee /usr/share/keyrings/cloudflare-main.gpg >/dev/null && \
    echo 'deb [signed-by=/usr/share/keyrings/cloudflare-main.gpg] https://pkg.cloudflare.com/cloudflared noble main' | tee /etc/apt/sources.list.d/cloudflared.list

RUN cat /usr/share/keyrings/cloudflare-main.gpg

RUN apt-get update && \
    apt-get -y install cloudflared

RUN cloudflared service install $CLOUDFLARE_TOKEN

COPY startup.sh /tmp/startup.sh
RUN chmod 744 /tmp/startup.sh
CMD ["/tmp/startup.sh"]