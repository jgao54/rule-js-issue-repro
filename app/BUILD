load("@aspect_rules_js//js:defs.bzl", "js_binary")
load("@aspect_rules_js//js:defs.bzl", "js_image_layer")
load("@aspect_bazel_lib//lib:utils.bzl", "to_label")
load("@io_bazel_rules_docker//container:container.bzl", "container_image", "container_layer")

js_binary(
	name = "main",
	data = ["//dep:rs_main"],
	entry_point = "main.js",
)

js_image_layer(
    name = "layers",
    binary = "main",
    visibility = ["//visibility:__pkg__"],
)

filegroup(
    name = "app_tar",
    srcs = [":layers"],
    output_group = "app",
)

container_layer(
    name = "app_layer",
    tars = [":app_tar"],
)

filegroup(
    name = "node_modules_tar",
    srcs = [":layers"],
    output_group = "node_modules",
)

container_layer(
    name = "node_modules_layer",
    tars = [":node_modules_tar"],
)

container_image(
    name = "image",
    base = "@base//image",
    entrypoint = "/bin/bash -c /app/main",
    layers = [
        ":node_modules_layer",
        ":app_layer",
    ],
    legacy_run_behavior = False,
)
