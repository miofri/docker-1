FROM ubuntu:focal

RUN apt-get update -q \
&& DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
busybox \
ca-certificates \
openssh-server \
tzdata \
curl \
gnupg \
apt-transport-https \
wget \
postfix \
&& rm -rf /var/lib/apt/lists/*

RUN curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
apt-get install -y gitlab-ce && \
rm -rf /var/lib/apt/lists/*

# '-batch'this sets the batch mode. In this mode no questions will be asked and all certificates will be certified automatically.
RUN mkdir -p /etc/gitlab/ssl \
&& chmod 755 /etc/gitlab/ssl \
&& openssl req -new -x509 -nodes -batch -newkey rsa:2048 -keyout /etc/gitlab/ssl/gitlab.key -out /etc/gitlab/ssl/gitlab.crt -days 365

RUN echo "external_url \"https://localhost\"" >> /etc/gitlab/gitlab.rb \
&& echo "nginx['ssl_certificate'] = \"/etc/gitlab/ssl/gitlab.crt\"" >> etc/gitlab/gitlab.rb \
&& echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/ssl/gitlab.key\"" >> /etc/gitlab/gitlab.rb \
&& echo "gitlab_rails['gitlab_shell_ssh_port'] = 22" >> /etc/gitlab/gitlab.rb

EXPOSE 80 443 22

RUN apt-get update && apt install software-properties-common -y && apt update

RUN add-apt-repository ppa:git-core/ppa \
&& apt-get update \
&& apt-get install git -y

#bypassing self-signed cert error
RUN git config --global http.sslverify false

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) \
&& service ssh start \
&& gitlab-ctl reconfigure \
&& gitlab-ctl tail

# docker build -t gitlab .
# docker run --rm -it -p 8443:443 -p 8022:22 --privileged gitlab

# When the container starts, it will run tail and starts logging. Open another container and exec into it when needed.
# go to localhost:8443 and login with root. passwd is in /etc/gitlab/initial_root_password

# Testing HTTPS
# create an empty repository in localhost:8443 & git clone. create a file and try git push.

# Testing ssh
# run ssh-keygen -t ed25519 (safer than RSA) and copy it to gitlab
# git clone like normal.

# -- INSTALLATION PACKAGE --
# non-interactive -> used when zero interaction while installing or upgrading the system via apt. It accepts the default answer for all questions. It might mail an error message to the root user. One can use such mode in Dockerfile, shell scripts, cloud-init script, and more.
# wget is basically curl, was in the official gitlab dockerfile
# busybox -> unix utilities like adduser, install,cat, etc.
# tzdata -> basically for timezones
# apt-transport-https -> allows the use of repositories accessed via https. Used only by apt tools and not the user.
# gnupg -> GnuPG allows you to encrypt and sign your data and communications

# -- GITLAB--
# /opt/gitlab/embedded/bin/runsvdir-start:
#	-> https://gitlab.com/gitlab-org/omnibus-gitlab/-/issues/4257#note_171862038
# gitlab-ctl reconfigure:
#	-> Reconfiguring GitLab should occur in the event that something in its configuration (/etc/gitlab/gitlab.rb) has changed.

# -- ENTRYPOINT AMPERSAND --
# An ampersand does the same thing as a semicolon or newline in that it indicates the end of a command, but it causes Bash to execute the command asynchronously. That means Bash will run it in the background and run the next command immediately after, without waiting for the former to end.

# https://www.howtoforge.com/tutorial/how-to-install-and-configure-gitlab-on-ubuntu-1804/