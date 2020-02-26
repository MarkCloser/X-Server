FROM  alpine:3.10

LABEL author 18222822278@163.com

COPY script/helloworld.py   /tmp/helloworld.py
COPY script/Python-3.8.2.tgz    /root/Python-3.8.2.tgz 
COPY script/pip.conf ~/.pip/pip.conf

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk add --no-cache tzdata \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone 

RUN apk add gcc libffi-dev python-dev openssl-dev make zlib-dev libc-dev


WORKDIR /root
RUN tar -zxvf Python-3.8.2.tgz  \
        && rm -rf Python-3.8.2.tgz  \
        && cd Python-3.8.2 \
        && ./configure \
        && make \
        && make install \
        && rm -rf /root/Python-3.8.2

RUN apk add --no-cache  tree vim

RUN pip3 install tornado

EXPOSE 8888

WORKDIR /tmp

CMD ["python3", "/tmp/helloworld.py"]
