FROM node:21-bookworm-slim

#Tell puppeteer to not download bundled chrome browser
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true

#Configure apt sources list with Google Repository to install google chrome
RUN apt-get update && apt-get install -y gnupg wget && \
    wget --quiet --output-document=- https://dl-ssl.google.com/linux/linux_signing_key.pub | gpg --dearmor > /etc/apt/trusted.gpg.d/google-chrome.gpg && \
    sh -c 'echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list' && \
    apt-get update && \
    apt-get install -y --no-install-recommends google-chrome-stable && \
    apt-get clean autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

#Add node user to audio and video groups
RUN usermod -aG audio,video node
USER node
