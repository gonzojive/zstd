# Bazel workspace for zstd. This file is used only for building zstd in
# isolation. To depend on zstd from other projects, support is forthcoming.
workspace(
    name = "com_github_facebook_zstd",
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# https://github.com/nelhage/rules_boost
#
# Only needed for org_lzma_lzma
http_archive(
    name = "com_github_nelhage_rules_boost",
    sha256 = "c1b8b2adc3b4201683cf94dda7eef3fc0f4f4c0ea5caa3ed3feffe07e1fb5b15",
    strip_prefix = "rules_boost-652b21e35e4eeed5579e696da0facbe8dba52b1f",
    urls = [
        "https://github.com/nelhage/rules_boost/archive/652b21e35e4eeed5579e696da0facbe8dba52b1f.tar.gz",
    ],
)

# From https://github.com/nelhage/rules_boost/blob/master/boost/boost.bzl
SOURCEFORGE_MIRRORS = ["phoenixnap", "newcontinuum", "cfhcable", "superb-sea2", "cytranet", "iweb", "gigenet", "ayera", "astuteinternet", "pilotfiber", "svwh"]

http_archive(
    name = "org_lzma_lzma",
    build_file = "@com_github_nelhage_rules_boost//:BUILD.lzma",
    sha256 = "71928b357d0a09a12a4b4c5fafca8c31c19b0e7d3b8ebb19622e96f26dbf28cb",
    strip_prefix = "xz-5.2.3",
    urls = [
        "https://%s.dl.sourceforge.net/project/lzmautils/xz-5.2.3.tar.gz" % m
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
