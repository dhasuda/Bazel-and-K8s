load("@io_bazel_rules_k8s//k8s:object.bzl", "k8s_object")

k8s_object(
  name = "namespace",
  cluster = "",
  template = "//k8s:namespace.yaml",
  visibility = ["//visibility:public"],
)

k8s_object(
  name = "service",
  cluster = "",
  template = "//k8s:service.yaml",
  images = {
    "docker.io/dhasuda/service-example:dev": "@image_example//:image",
  },
  visibility = ["//visibility:public"],
)