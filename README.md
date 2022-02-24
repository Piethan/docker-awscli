[![Dockerhub](https://img.shields.io/badge/Dockerhub-ccdirk/awscli-blue)](https://hub.docker.com/r/ccdirk/awscli)
[![GitHub](https://img.shields.io/badge/github-docker--awscli-blue)](https://github.com/Piethan/docker-awscli)

# docker-awscli

## example with scp

```shell
docker run --rm -it --env-file <(aws-vault exec default -- env | grep --color=never ^AWS_) -v $HOME/.ssh:/root/.ssh --entrypoint /usr/bin/scp ccdirk/awscli:latest  -i /root/.ssh/id_rsa ec2-user@i-XXXXXXXXXX:/home/ec2-user/.htaccess .
```

## example with ssh

```shell
docker run --rm -it --env-file <(aws-vault exec default -- env | grep --color=never ^AWS_) -v $HOME/.ssh:/root/.ssh --entrypoint /usr/bin/ssh ccdirk/awscli:latest i-XXXXXXXXXX -l ec2-user -i /root/.ssh/id_rsa
```