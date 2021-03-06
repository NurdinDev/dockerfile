FROM php:7.4-cli-stretch

# Apt and common dependencies
RUN apt-get update && apt-get install -y \
    # Commons
    sudo \
    autogen \
    wget \
    zip \
    unzip \
    tar \
    git \
    subversion \
    build-essential \
    apt-utils \
    software-properties-common \
    nasm \
    libjpeg-dev \
    libpng-dev \
    libpng16-16 \
    # Allow simple FTP uploads
    lftp \
    wput \
    # Pyhton is needed for Docker-Compose
    python \
    python-pip \
    python-dev \
    # Cypress.io dependencies
    xvfb \
    libgtk2.0-0 \
    libgtk-3-0 \
    libnotify-dev \
    libgconf-2-4 \
    libnss3 \
    libxss1 \
    libasound2 \
    libxtst6 \
    xauth \
    # libssl-dev is needed for Phar (https://raspberrypi.stackexchange.com/a/36379)
    libssl-dev && \
    # PHP dependencies (https://git.io/JvAFa)
    docker-php-ext-install -j4 phar json mbstring tokenizer && \
    # xdebug (can be activated with `docker-php-ext-enable xdebug`, not by default because it slows down PHP)
    pecl install xdebug && \
    # Composer
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer && \
    composer self-update && \
    # Node
    curl -sL https://deb.nodesource.com/setup_12.x -o nodesource_setup.sh && \
    bash nodesource_setup.sh && \
    apt-get install -y nodejs && \
    # Yarn
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn && \
    # Docker and Docker-Compose (via Python, PiP)
    curl -sSL https://get.docker.com/ | sh && \
    pip install docker-compose && \
    # WP CLI
    curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    php wp-cli.phar --info && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp && \
    # PHP Scoper
    curl -O -L https://github.com/humbug/php-scoper/releases/download/0.13.1/php-scoper.phar && \
    chmod +x php-scoper.phar && \
    mv php-scoper.phar /usr/local/bin/php-scoper

RUN npm install -g \
    # Global installations of npm packages
    wait-on
    # && \
    # composer global require \
    # Global installations of composer packages
    # hirak/prestissimo Prestissimo is currently not possible together with Lerna and CI due to a RC (https://git.io/JvPkZ)... wait for Composer v2
