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


## example gitlab pipeline
```yaml
variables:
   AWS_ACCESS_KEY_ID: $AWS_ACCESS_KEY_ID
   AWS_DEFAULT_REGION: $AWS_DEFAULT_REGION
   AWS_SECRET_ACCESS_KEY: $AWS_SECRET_ACCESS_KEY
   DEPLOYER_KEY: $DEPLOYER_KEY

stages:
  - prod

copy_htaccess:
  stage: prod
  image:
    name: ccdirk/awscli:latest
    entrypoint: [""]
  script:
    -  echo "$DEPLOYER_KEY" > /root/.ssh/key
    -  chmod 0600 /root/.ssh/key
    -  chmod 666 /dev/tty
    -  scp -i /root/.ssh/key -o "StrictHostKeyChecking=no" -vvvv .htaccess ec2-user@i-XXXXXXXXXXXX:/home/ec2-user/.htaccess
    -  ssh -i /root/.ssh/key -o "StrictHostKeyChecking=no" -vvvv -l ec2-user i-XXXXXXXXXXX 'sudo cp /home/ec2-user/.htaccess /var/www/html/web/.htaccess && sudo chmod 0644 /var/www/html/web/.htaccess'


```