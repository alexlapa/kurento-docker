FROM kurento/kurento-media-server:6.7.2-xenial

RUN cd \tmp \
  && apt-get update \
  && deps=" \
          autotools-dev \
          cdbs \
          dh-autoreconf \
          libglib2.0-dev \
          gtk-doc-tools \
          libgnutls-dev\
      " \
  && apt-get install -y --no-install-recommends --no-install-suggests \
          $deps\
  && wget -O libnice.tar.gz https://github.com/alexlapa/libnice/archive/master.tar.gz \
  && tar -xvzf libnice.tar.gz \
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
             /tmp/*