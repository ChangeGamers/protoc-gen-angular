config_setting(
	name = "msvc",
	values = {
		"cpu": "x64_windows",
	},
	visibility = ["//:__subpackages__"],
)

CXX17_COPT = select({
	":msvc": ["/std:c++17"],
  "//conditions:default": ["-std=c++17"],
})

cc_binary(
  name = "protoc-gen-angular",
  srcs = [
    "generator.cc",
    "generator.h",
    "main.cc",
  ],
  deps = [
    "@com_google_protobuf//:protoc_lib"
  ],
  copts = [] + CXX17_COPT,
)
