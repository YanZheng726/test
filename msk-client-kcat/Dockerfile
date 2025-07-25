FROM public.ecr.aws/docker/library/debian:bullseye-slim

RUN apt-get update && apt-get install -y \
  curl \
  jq \
  unzip \
  netcat \
  librdkafka-dev \
  build-essential \
  git \
  ca-certificates \
  python3 \
  python3-pip \
  && rm -rf /var/lib/apt/lists/*

# 安装kcat
RUN curl -L https://github.com/edenhill/kcat/releases/download/1.7.1/kcat-1.7.1.tar.gz | tar xz && \
    cd kcat-1.7.1 && \
    ./configure && make && make install

# 安装MSK IAM lib
RUN curl -Lo aws-msk-iam-auth.zip https://github.com/aws/aws-msk-iam-auth/releases/latest/download/aws-msk-iam-auth-1.1.2.zip && \
    unzip aws-msk-iam-auth.zip -d /opt/aws-msk && \
    chmod +x /opt/aws-msk/aws-msk-iam-auth-1.1.2/aws-msk-iam-auth

ENV LD_LIBRARY_PATH=/opt/aws-msk/aws-msk-iam-auth-1.1.2

ENTRYPOINT [ "kcat" ]
