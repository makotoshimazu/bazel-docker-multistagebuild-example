load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_image",
)
load(
    "@io_bazel_rules_docker//docker/util:run.bzl",
    "container_run_and_extract",
)

# The files used by the base image.
filegroup(
    name = "scripts",
    srcs = [
        "scripts/sample.sh",
    ],
    visibility = ["//visibility:private"],
)

# Create a container image: progatepath/simple:build_image.
container_image(
    name = "build_image",
    base = "@alpine_linux_amd64//image",
    data_path = ".",
    directory = "/workspace",
    entrypoint = ["/workspace/scripts/sample.sh"],
    files = [
        ":scripts",
    ],
    repository = "progatepath",
)

# Run progatepath/simple:build_image and extract a file `/workspace/hello.sh`
# as the build output.
# You can try `bazel build //simple:build` and see the path to the extracted
# file by the following command:
#
# $ bazel cquery //simple:build/workspace/hello.sh --output starlark \
#     --starlark:expr="target.files.to_list()[0].path" 2>/dev/null
#
container_run_and_extract(
    name = "build",
    commands = ["echo do nothing."],
    extract_file = "/workspace/scripts/sample.sh",
    # Use the layer generated by `container_image` rule.
    image = ":build_image.tar",
)

# You can build and run a image by this simgle command:
#
# $ bazel run //simple:image
container_image(
    name = "image",
    base = "@alpine_linux_amd64//image",
    cmd = [
        "-c",
        "nc -vl -p 8081 < /workspace/somefiles/hello.txt",
    ],
    # It puts files relative to the workspace.
    # hello.sh goes to `/workspace/simple/build/workspace/hello.sh`.
    data_path = "/",
    directory = "/workspace",
    # Expose the port when running the docker image.
    docker_run_flags = "-p 8081:8081",
    entrypoint = ["/bin/sh"],
    files = [
        ":build/workspace/scripts/sample.sh",
        "//somefiles:textfiles",
    ],
    # Set to false to run the docker image on `bazel run`.
    legacy_run_behavior = False,
    repository = "progatepath",
    stamp = "@io_bazel_rules_docker//stamp:always",
)
