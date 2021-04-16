FROM node:14.16.0-buster
RUN apt-get update
RUN apt-get install git -y --no-install-recommends
RUN git clone https://github.com/deltachat/deltachat-desktop.git
WORKDIR ./deltachat-desktop
RUN npm install -verbose
#RUN apt-get install -y libnss3-tools; \
#    apt-get install -y libatk1.0-0
#RUN apt-get install -y libatk-bridge2.0-0
#RUN apt-get install -y gconf-service libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxss1 libxtst6 libappindicator1 libnss3 libasound2 libatk1.0-0 libc6 ca-certificates fonts-liberation lsb-release xdg-utils wget
#RUN apt-get install -y libgbm-dev
RUN npm run build
RUN npm start
