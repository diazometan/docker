FROM ubuntu:16.04

RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y ca-certificates openssh-server wget

RUN wget \
 	https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh \
	&& chmod 777 script.deb.sh \
	&& ./script.deb.sh \
	&& apt-get install -y tzdata gitlab-ce \
	&& mkdir -p /etc/gitlab/ssl \
	&& chmod 755 /etc/gitlab/ssl \
	&& echo external_url \"https://gitlab.example.com\" > ./etc/gitlab/gitlab.rb \
	&& echo nginx[\'ssl_certificate\'] = \"/etc/gitlab/ssl/gitlab.example.com.crt\" >> ./etc/gitlab/gitlab.rb \
	&& echo nginx[\'ssl_certificate_key\'] = \"/etc/gitlab/ssl/gitlab.example.com.key\" >> ./etc/gitlab/gitlab.rb

WORKDIR /etc/gitlab/ssl

RUN openssl req -newkey rsa:2048 -nodes \
	-keyout gitlab.example.com.key -x509 \
	-days 365 -out gitlab.example.com.crt \
	-subj "/C=GB/ST=London/L=London/O=Global Security/OU=IT Department/CN=gitlab.example.com"

EXPOSE 443 80 22

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) \
			&& service ssh start \
			&& gitlab-ctl reconfigure \
			&& tail -f /dev/null


# How to build it?
# docker build -t ex03 .

# How to run it?
# docker run -it --rm -p 8080:80 -p 8022:22 -p 8443:443 --privileged ex03
