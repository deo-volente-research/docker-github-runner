FROM getsentry/sentry-cli:latest as sentry-cli

FROM ubuntu:jammy

#Setup OS
RUN apt update -y && apt -y upgrade && apt install lsb-release ca-certificates apt-transport-https software-properties-common wget -y

#Add Sentry CLI
COPY --from=sentry-cli /bin/sentry-cli /bin

#Install PHP ondrej
RUN add-apt-repository ppa:ondrej/php -y

#Fetch latest packages
RUN apt update -y

#Install tzdata
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends tzdata

#Install Packages
RUN apt install --no-install-recommends --yes php8.1-cli php8.1-fpm php8.1-common php8.1-bcmath php8.1-curl php8.1-imagick php8.1-mbstring php8.1-pdo-mysql php8.1-zip php8.1-amqp php8.1-gd php8.1-redis php8.1-soap php8.1-xml php8.1-intl php8.1-dom composer nginx sudo curl git python3-pip rename fonts-roboto-unhinted xvfb mysql-client rabbitmq-server openssh-client
RUN pip3 install awscli

#Install NodeJS
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - && sudo apt-get install -y nodejs

#Install Yarn
RUN curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | sudo tee /usr/share/keyrings/yarnkey.gpg >/dev/null && echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt-get update && sudo apt-get install yarn

#Install chrome
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && apt install --yes ./google-chrome-stable_current_amd64.deb

#Setup PHP
RUN sed -i 's/memory_limit = 128M/memory_limit = 4096M/g' /etc/php/8.1/cli/php.ini

# Make cache dir for applications available
RUN mkdir -p /var/www/.cache && chmod 777 /var/www/.cache

#Make php8.1 default
RUN update-alternatives --set php /usr/bin/php8.1

#Disable github dubious owner checks
RUN git config --system --add safe.directory '*'
