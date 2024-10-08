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
RUN apt install --no-install-recommends --yes composer nginx sudo curl git python3-pip rename fonts-roboto-unhinted xvfb mysql-client rabbitmq-server openssh-client mysql-server

#Install PHP8.1
RUN apt install --no-install-recommends --yes  php8.1-cli php8.1-fpm php8.1-common php8.1-bcmath php8.1-curl php8.1-imagick php8.1-mbstring php8.1-pdo-mysql php8.1-sqlite3 php8.1-zip php8.1-amqp php8.1-gd php8.1-redis php8.1-soap php8.1-xml php8.1-intl php8.1-dom

#Install PHP8.3
RUN apt install --no-install-recommends --yes  php8.3-cli php8.3-fpm php8.3-common php8.3-bcmath php8.3-curl php8.3-imagick php8.3-mbstring php8.3-pdo-mysql php8.3-sqlite3 php8.3-zip php8.3-amqp php8.3-gd php8.3-redis php8.3-soap php8.3-xml php8.3-intl php8.3-dom

#Install AWSCLI
RUN pip3 install awscli

#Install NodeJS
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - && sudo apt-get install -y nodejs

#Install Yarn
RUN curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | sudo tee /usr/share/keyrings/yarnkey.gpg >/dev/null && echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt-get update && sudo apt-get install yarn

#Install playwright dependencies
RUN apt install --no-install-recommends --yes xvfb fonts-noto-color-emoji fonts-unifont libfontconfig1 libfreetype6 xfonts-cyrillic xfonts-scalable fonts-liberation fonts-ipafont-gothic fonts-wqy-zenhei fonts-tlwg-loma-otf fonts-freefont-ttf libasound2 libatk-bridge2.0-0 libatk1.0-0 libatspi2.0-0 libcairo2 libcups2 libdbus-1-3 libdrm2 libgbm1 libglib2.0-0 libnspr4 libnss3 libpango-1.0-0 libwayland-client0 libx11-6 libxcb1 libxcomposite1 libxdamage1 libxext6 libxfixes3 libxkbcommon0 libxrandr2 ffmpeg libasound2 libatk1.0-0 libcairo-gobject2 libcairo2 libdbus-1-3 libdbus-glib-1-2 libfontconfig1 libfreetype6 libgdk-pixbuf-2.0-0 libglib2.0-0 libgtk-3-0 libpango-1.0-0 libpangocairo-1.0-0 libx11-6 libx11-xcb1 libxcb-shm0 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxtst6 libsoup-3.0-0 libenchant-2-2 gstreamer1.0-libav gstreamer1.0-plugins-bad gstreamer1.0-plugins-base gstreamer1.0-plugins-good libicu70 libatk-bridge2.0-0 libatk1.0-0 libcairo2 libdbus-1-3 libdrm2 libegl1 libepoxy0 libevdev2 libffi7 libfontconfig1 libfreetype6 libgbm1 libgdk-pixbuf-2.0-0 libgles2 libglib2.0-0 libglx0 libgstreamer-gl1.0-0 libgstreamer-plugins-base1.0-0 libgstreamer1.0-0 libgtk-3-0 libgudev-1.0-0 libharfbuzz-icu0 libharfbuzz0b libhyphen0 libjpeg-turbo8 liblcms2-2 libmanette-0.2-0 libnotify4 libopengl0 libopenjp2-7 libopus0 libpango-1.0-0 libpng16-16 libproxy1v5 libsecret-1-0 libwayland-client0 libwayland-egl1 libwayland-server0 libwebpdemux2 libwoff1 libx11-6 libxcomposite1 libxdamage1 libxkbcommon0 libxml2 libxslt1.1 libx264-163 libatomic1 libevent-2.1-7

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
