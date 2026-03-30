FROM rust:1-trixie

# Node.js LTS via nvm for CI action runners (checkout, cache, artifacts)
ENV NVM_DIR=/usr/local/nvm
RUN mkdir -p "$NVM_DIR" \
    && curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash \
    && . "$NVM_DIR/nvm.sh" \
    && nvm install --lts \
    && nvm alias default lts/* \
    && nvm use default

# Make node/npm available system-wide
RUN ln -sf "$(ls -d $NVM_DIR/versions/node/v*)/bin/node" /usr/local/bin/node \
    && ln -sf "$(ls -d $NVM_DIR/versions/node/v*)/bin/npm" /usr/local/bin/npm

# Clippy for linting
RUN rustup component add clippy

# Verify
RUN rustc --version && cargo --version && node --version && npm --version
