load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# ---------------- Docker ----------------
http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "b1e80761a8a8243d03ebca8845e9cc1ba6c82ce7c5179ce2b295cd36f7e394bf",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.25.0/rules_docker-v0.25.0.tar.gz"],
)

# OPTIONAL: Call this to override the default docker toolchain configuration.
# This call should be placed BEFORE the call to "container_repositories" below
# to actually override the default toolchain configuration.
# Note this is only required if you actually want to call
# docker_toolchain_configure with a custom attr; please read the toolchains
# docs in /toolchains/docker/ before blindly adding this to your WORKSPACE.
# BEGIN OPTIONAL segment:
# load("@io_bazel_rules_docker//toolchains/docker:toolchain.bzl",
#     docker_toolchain_configure="toolchain_configure"
# )
# docker_toolchain_configure(
#   name = "docker_config",
#   # OPTIONAL: Bazel target for the build_tar tool, must be compatible with build_tar.py
#   build_tar_target="<enter absolute path (i.e., must start with repo name @...//:...) to an executable build_tar target>",
#   # OPTIONAL: Path to a directory which has a custom docker client config.json.
#   # See https://docs.docker.com/engine/reference/commandline/cli/#configuration-files
#   # for more details.
#   client_config="<enter Bazel label to your docker config.json here>",
#   # OPTIONAL: Path to the docker binary.
#   # Should be set explicitly for remote execution.
#   docker_path="<enter absolute path to the docker binary (in the remote exec env) here>",
#   # OPTIONAL: Path to the gzip binary.
#   gzip_path="<enter absolute path to the gzip binary (in the remote exec env) here>",
#   # OPTIONAL: Bazel target for the gzip tool.
#   gzip_target="<enter absolute path (i.e., must start with repo name @...//:...) to an executable gzip target>",
#   # OPTIONAL: Path to the xz binary.
#   # Should be set explicitly for remote execution.
#   xz_path="<enter absolute path to the xz binary (in the remote exec env) here>",
#   # OPTIONAL: Bazel target for the xz tool.
#   # Either xz_path or xz_target should be set explicitly for remote execution.
#   xz_target="<enter absolute path (i.e., must start with repo name @...//:...) to an executable xz target>",
#   # OPTIONAL: List of additional flags to pass to the docker command.
#   docker_flags = [
#     "--tls",
#     "--log-level=info",
#   ],
# )
# End of OPTIONAL segment.

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)

container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

# load(
#     "@io_bazel_rules_docker//container:container.bzl",
#     "container_pull",
# )

# container_pull(
#     name = "java_base",
#     # 'tag' is also supported, but digest is encouraged for reproducibility.
#     digest = "sha256:deadbeef",
#     registry = "gcr.io",
#     repository = "distroless/java",
# )

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
)

container_pull(
    name = "alpine_linux_amd64",
    registry = "index.docker.io",
    repository = "library/alpine",
    tag = "3.16",
)
