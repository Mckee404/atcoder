FROM mcr.microsoft.com/devcontainers/base:jammy

RUN apt update \
  && apt install -y build-essential gdb \
  && rm -rf /var/lib/apt/lists/*

# 先に作業ディレクトリを用意して所有者をvscodeに
RUN mkdir -p /workspace && chown -R vscode:vscode /workspace

# 所有者を維持したままコピー
COPY --chown=vscode:vscode . /workspace
WORKDIR /workspace

RUN git clone --depth 1 https://github.com/atcoder/ac-library.git /tmp/ac-library \
  && cd /tmp/ac-library \
  && [ "$ACL_COMMIT" = "master" ] || git fetch origin "$ACL_COMMIT" && git checkout "$ACL_COMMIT" || true \
  && mkdir -p /usr/local/include/atcoder \
  && cp -r atcoder/* /usr/local/include/atcoder/ \
  && rm -rf /tmp/ac-library