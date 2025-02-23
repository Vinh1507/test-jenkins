FROM jenkins/jenkins:lts
USER root

# Cài đặt các gói cần thiết
RUN apt-get update -qq && apt-get install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2

# Thêm khóa GPG và repo Docker
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN echo "deb [arch=amd64] https://download.docker.com/linux/debian bullseye stable" > /etc/apt/sources.list.d/docker.list

# Cài đặt Docker
RUN apt-get update -qq && apt-get install -y docker-ce

# Cài đặt Ansible
RUN apt-get update -qq && apt-get install -y ansible && apt-get clean

# Thêm quyền Docker cho user Jenkins
RUN usermod -aG docker jenkins
