FROM node:24-alpine
LABEL maintainer="security@khulnasoft.com"

ARG MODD_VERSION
ARG TASKFILE_VERSION

# Tell Puppeteer to skip installing Chrome. We'll be using the installed package.
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true

# Based on: https://github.com/GoogleChrome/puppeteer/blob/master/docs/troubleshooting.md#running-on-alpine

# Installs Chromium 72 package.
RUN apk update && apk upgrade && \
    apk add --no-cache \
      chromium \
      harfbuzz \
      freetype \
      ttf-freefont \
      nss && \
    # Puppeteer v1.11.0 works with Chromium 72.
    yarn add puppeteer@1.13.0 && \
    apk add --update curl git grep make ncurses tzdata && \
    echo "Install Taskfile" && \
    curl -sSL https://taskfile.dev/install.sh | sh -s v${TASKFILE_VERSION} && \
    echo "Done Install Taskfile" && \
    echo "Adding an up to date mime-types definition file" && \
    curl -sSL https://salsa.debian.org/debian/mime-support/raw/master/mime.types -o /etc/mime.types && \
    echo "Linking the Chrome executable with all the known/used names" && \
    ln -s /usr/bin/chromium-browser /usr/bin/google-chrome && \
    ln -s /usr/bin/chromium-browser /usr/bin/google-chrome-unstable && \
    rm -rf /tmp/* /var/cache/apk/*
