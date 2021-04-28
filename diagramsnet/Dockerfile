FROM debian:10.9-slim

ENV DRAWIO_VERSION "14.5.1"

RUN groupadd --gid 1000 kroki && useradd -r -g kroki -u 1000 kroki

WORKDIR /usr/local/kroki

RUN apt-get update && apt-get install -y \
  libappindicator3-1 \
  libatspi2.0-0 \
  libasound2 \
  libgconf-2-4 \
  libgtk-3-0 \
  libnotify4 \
  libnss3 \
  libsecret-1-0 \
  libxss1 \
  libxtst6 \
  libgbm-dev \
  wget \
  xdg-utils \
  xvfb \
  && wget -q https://github.com/jgraph/drawio-desktop/releases/download/v${DRAWIO_VERSION}/drawio-amd64-${DRAWIO_VERSION}.deb \
  && dpkg -i /usr/local/kroki/drawio-amd64-${DRAWIO_VERSION}.deb \
  && rm -f /usr/local/kroki/drawio-amd64-${DRAWIO_VERSION}.deb \
  && rm -rf /var/lib/apt/lists/*

COPY scripts/* ./

ENV ELECTRON_DISABLE_SECURITY_WARNINGS "true"
ENV DRAWIO_DISABLE_UPDATE "true"
ENV DRAWIO_DESKTOP_COMMAND_TIMEOUT "10s"
ENV DRAWIO_DESKTOP_EXECUTABLE_PATH "/opt/drawio/drawio"
# Currently, no security warning in this version of drawio desktop
# ENV DRAWIO_DESKTOP_RUNNER_COMMAND_LINE "/usr/local/kroki/runner.sh"
ENV DRAWIO_DESKTOP_RUNNER_COMMAND_LINE "/usr/local/kroki/runner-no-security-warnings.sh"
ENV XVFB_DISPLAY ":42"
ENV XVFB_OPTIONS ""

#USER kroki

ENTRYPOINT [ "/usr/local/kroki/entrypoint.sh" ]
CMD [ "--help" ]
