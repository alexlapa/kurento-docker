FROM kurento/kurento-media-server:6.7.2-xenial

RUN apt-get update \
  && apt-get upgrade -y \
  && deps=" \
          unzip \
          autotools-dev \
          cdbs \
          dh-autoreconf \
          libglib2.0-dev \
          gtk-doc-tools \
          libgnutls-dev\
      " \
  && apt-get install -y --no-install-recommends --no-install-suggests \
          $deps\
  && wget -O libnice.zip https://github.com/alexlapa/libnice/archive/master.zip \
  && unzip libnice.zip \
  && cd libnice-master \
  && ./autogen.sh \
  && ./configure --libdir=/usr/lib/x86_64-linux-gnu/ \
  && make \
  && make install \
  && apt-get clean \
  # Cleanup unnecessary stuff
  && apt-get purge -y --auto-remove \
                    -o APT::AutoRemove::RecommendsImportant=false \
              $deps \
  && rm -rf /var/lib/apt/lists/* \
             /etc/*/inetutils-syslogd \
             /tmp/*