load("@io_bazel_rules_docker//container:container.bzl", "container_image")

load("@rules_pkg//:pkg.bzl", "pkg_tar")
load("@io_bazel_rules_docker//docker/util:run.bzl", "container_run_and_commit")

pkg_tar(
    name = "src-tar",
    srcs = glob(["src/**"]),
    # Otherwise all directories are flattened:
    # <https://github.com/bazelbuild/rules_docker/issues/317>
    strip_prefix = ".",
)

genrule(
  name = "dockerfile",
  srcs = [
      "//:package.json",
      "//:tsconfig.json",
      "//:Dockerfile",
      "//:yarn.lock",
      ":src-tar",
    ],
  cmd = "tar -czh . | docker build -q -t image-test -f $(location Dockerfile) --build-arg yarnlock=$(location yarn.lock) --build-arg tsconfig=$(location tsconfig.json) --build-arg src=$(location :src-tar) --build-arg package=$(location package.json) --build-arg yarnlock=$(location yarn.lock) --build-arg tsconfig=$(location tsconfig.json) - && docker save --output $@ image-test",
  outs = ["image-test.tar"],
)

container_image(
    name = "image",
    base = "//:dockerfile",
    visibility = ["//visibility:public"],
)