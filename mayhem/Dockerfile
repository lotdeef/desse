# ARGS
ARG project=desse

# Setup Fuzz-Rust Builder
FROM ghcr.io/nottirb/fuzz-rust:latest as builder
ADD . /${project}
WORKDIR /${project}
RUN cd ./fuzz && cargo +nightly hfuzz build

# Setup Fuzz-Env
FROM ghcr.io/nottirb/fuzz-env:latest
COPY --from=builder ${project}/fuzz/hfuzz_target/x86_64-unknown-linux-gnu/release/deserialize /
COPY --from=builder ${project}/fuzz/hfuzz_target/x86_64-unknown-linux-gnu/release/round_trip /
COPY --from=builder ${project}/fuzz/hfuzz_target/x86_64-unknown-linux-gnu/release/serialize /
