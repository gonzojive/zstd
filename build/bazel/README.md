This directory contains files for building zstd with BAZEL.

To use zstd from another bazel project, add the following to your
WORKSPACE:

```starlark
# zstd:
http_archive(
    name = "com_github_facebook_zstd",
    sha256 = "9092a91a415eeb509316e41e29a8ddcc2ac2af352d654c7c2c3fff3b2092d90e",
    strip_prefix = "zstd-6640377783e73211d1afd440550f8587dd9de75c",
    urls = [
        "https://github.com/facebook/zstd/archive/6640377783e73211d1afd440550f8587dd9de75c.tar.gz",
    ],
    build_file = "@com_github_facebook_zstd//build/bazel:zstd.BUILD",
)

# dependencies of zstd:

http_archive(
    name = "bazel_skylib",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.3.0/bazel-skylib-1.3.0.tar.gz",
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.3.0/bazel-skylib-1.3.0.tar.gz",
    ],
    sha256 = "74d544d96f4a5bb630d465ca8bbcfe231e3594e5aae57e1edbf17a6eb3ca2506",
)
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

# https://github.com/nelhage/rules_boost
#
# Only needed for org_lzma_lzma
http_archive(
    name = "com_github_nelhage_rules_boost",
    sha256 = "9092a91a415eeb509316e41e29a8ddcc2ac2af352d654c7c2c3fff3b2092d90e",
    strip_prefix = "rules_boost-c5593c88c840ac9b2251b8514aeb622ef7dc91a4",
    urls = [
        "https://github.com/nelhage/rules_boost/archive/c5593c88c840ac9b2251b8514aeb622ef7dc91a4.tar.gz",
    ],
)

# From https://github.com/nelhage/rules_boost/blob/master/boost/boost.bzl
SOURCEFORGE_MIRRORS = ["phoenixnap", "newcontinuum", "cfhcable", "superb-sea2", "cytranet", "iweb", "gigenet", "ayera", "astuteinternet", "pilotfiber", "svwh"]

http_archive(
    name = "org_lzma_lzma",
    build_file = "@com_github_nelhage_rules_boost//:BUILD.lzma",
    sha256 = "06327c2ddc81e126a6d9a78b0be5014b976a2c0832f492dcfc4755d7facf6d33",
    strip_prefix = "xz-5.2.7",
    urls = [
        "https://%s.dl.sourceforge.net/project/lzmautils/xz-5.2.7.tar.gz" % m
        for m in SOURCEFORGE_MIRRORS
    ],
)

http_archive(
    name = "lz4",
    build_file = "@com_github_facebook_zstd//build/bazel:lz4.BUILD",
    patch_cmds = [
        """sed -i.bak 's/__attribute__ ((__visibility__ ("default")))//g' lib/lz4frame.h """,
    ],
    sha256 = "658ba6191fa44c92280d4aa2c271b0f4fbc0e34d249578dd05e50e76d0e5efcc",
    strip_prefix = "lz4-1.9.2",
    urls = [
        "https://storage.googleapis.com/mirror.tensorflow.org/github.com/lz4/lz4/archive/v1.9.2.tar.gz",
        "https://github.com/lz4/lz4/archive/v1.9.2.tar.gz",
    ],
)
```
