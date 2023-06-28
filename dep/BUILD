load("@rules_rust//rust:defs.bzl", "rust_library")

cc_library(
    name = "c_main",
    srcs = ["main.c"],
    visibility = ["//visibility:public"],
)

rust_library(
    name = "rs_main",
    srcs = ["main.rs"],
    deps = [":c_main"],
    visibility = ["//visibility:public"],
)
