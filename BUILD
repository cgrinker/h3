genrule(
    name = "gen_sh",
    outs = [
        "gen.sh",
    ],
    cmd = """
cat > $@ <<"EOF"
#! /bin/sh
sed -e 's/@H3_VERSION_MAJOR@/1/g' \
    -e 's/@H3_VERSION_MINOR@/1/g' \
    -e 's/@H3_VERSION_PATCH@/0/g'
EOF""",
)
genrule(
    name = "h3api_h",
    srcs = ["src/h3lib/include/h3api.h.in"],
    outs = ["src/h3lib/include/h3api.h"],
    cmd = "$(location :gen_sh) < $(<) > $(@)",
    tools = [":gen_sh"],
)

cc_library(
  name = "h3",
  visibility = ["//visibility:public"],
  includes = [
    "src/h3lib/include"
  ],
  hdrs = [":h3api_h"] + glob([
     "src/h3lib/include/*.h"
  ]),
  srcs = glob([
      "src/h3lib/lib/*.c*"
  ])
)