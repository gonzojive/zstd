# Description:
#   LZ4 library
#
# From https://github.com/tensorflow/io/blob/master/third_party/lz4.BUILD.

licenses(["notice"])  # BSD license

exports_files(["LICENSE"])

cc_library(
    name = "lz4",
    srcs = [
        "lib/lz4.c",
        "lib/lz4.h",
        "lib/lz4frame.c",
        "lib/lz4frame.h",
        "lib/lz4hc.h",
        "lib/lz4hc.c",
        "lib/xxhash.h",
    ],
    hdrs = [],
    local_defines = [
        "XXH_PRIVATE_API",
        "LZ4LIB_VISIBILITY=",
    ],
    includes = [
        "lib",
    ],
    linkopts = [],
    textual_hdrs = [
        "lib/xxhash.c",
        "lib/lz4.c",
    ],
    visibility = ["//visibility:public"],
)
