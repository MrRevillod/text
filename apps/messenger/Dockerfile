FROM rust:1.84-bullseye

RUN cargo install cargo-watch

WORKDIR /social-net

COPY Cargo.toml Cargo.lock ./

COPY libs/common/Cargo.toml ./libs/common/Cargo.toml
COPY libs/prisma_cli/Cargo.toml ./libs/prisma_cli/Cargo.toml

COPY apps/auth/Cargo.toml ./apps/auth/Cargo.toml
COPY apps/messenger/Cargo.toml ./apps/messenger/Cargo.toml

RUN mkdir -p ./apps/auth/src && echo 'fn main() {}' > ./apps/auth/src/main.rs
RUN mkdir -p ./apps/messenger/src && echo 'fn main() {}' > ./apps/messenger/src/main.rs

RUN mkdir -p ./libs/common/src && echo 'fn main() {}' > ./libs/common/src/lib.rs
RUN mkdir -p ./libs/prisma_cli/src && echo 'fn main() {}' > ./libs/prisma_cli/src/lib.rs

RUN cargo build --release -p messenger

RUN rm -rf ./apps
RUN rm -rf ./libs

COPY libs ./libs
COPY apps ./apps

WORKDIR /social-net/apps/messenger

EXPOSE 8000

CMD ["cargo", "watch", "-x", "run"]