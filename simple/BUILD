load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_image",
)

container_image(
    name = "image",
    base = "@alpine_linux_amd64//image",
    cmd = [
        "hello",
        "world",
    ],
    entrypoint = ["echo"],
    repository = "progatepath",
)
