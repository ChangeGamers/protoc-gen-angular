workspace(
    name = "com_github_zaucy_protoc_gen_angular",
    managed_directories = {"@npm": ["node_modules"]},
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")


http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "d63ecec7192394f5cc4ad95a115f8a6c9de55c60d56c1f08da79c306355e4654",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/4.6.1/rules_nodejs-4.6.1.tar.gz"],
)

http_archive(
    name = "io_bazel_rules_sass",
    sha256 = "4c87befcb17282b039ba8341df9a6cc45f461bf05776dcf35c7e40c7e79ce374",
    strip_prefix = "rules_sass-3a4f31c74513ccfacce3f955b5c006352f7e9587",
    url = "https://github.com/bazelbuild/rules_sass/archive/3a4f31c74513ccfacce3f955b5c006352f7e9587.zip",
)

# The yarn_install rule runs yarn anytime the package.json or yarn.lock file
# changes. It also extracts and installs any Bazel rules distributed in an npm
# package.
load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")
yarn_install(
    # Name this npm so that Bazel Label references look like @npm//package
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

# Install any Bazel rules which were extracted earlier by the yarn_install rule.
load("@npm//:install_bazel_dependencies.bzl", "install_bazel_dependencies")
install_bazel_dependencies()

# Load karma dependencies
load("@npm_bazel_karma//:package.bzl", "npm_bazel_karma_dependencies")
npm_bazel_karma_dependencies()

# Setup the rules_webtesting toolchain
load(
    "@io_bazel_rules_webtesting//web:repositories.bzl", 
    "web_test_repositories",
)
web_test_repositories()

load(
    "@io_bazel_rules_webtesting//web/versioned:browsers-0.3.1.bzl", 
    "browser_repositories",
)
browser_repositories()

# Setup the rules_typescript tooolchain
load("@npm_bazel_typescript//:index.bzl", "ts_setup_workspace")
ts_setup_workspace()

# Setup the rules_sass toolchain
load("@io_bazel_rules_sass//sass:sass_repositories.bzl", "sass_repositories")
sass_repositories()

http_archive(
    name = "com_google_protobuf",
    sha256 = "b7220b41481011305bf9100847cf294393973e869973a9661046601959b2960b",
    strip_prefix = "protobuf-3.8.0",
    urls = ["https://github.com/protocolbuffers/protobuf/releases/download/v3.8.0/protobuf-all-3.8.0.tar.gz"],
)

http_archive(
    name = "zlib",
    build_file = "@com_google_protobuf//:third_party/zlib.BUILD",
    sha256 = "c3e5e9fdd5004dcb542feda5ee4f0ff0744628baf8ed2dd5d66f8ca1197cb1a1",
    strip_prefix = "zlib-1.2.11",
    urls = ["https://zlib.net/zlib-1.2.11.tar.gz"],
)

http_archive(
    name = "rules_proto_grpc",
    sha256 = "8383116d4c505e93fd58369841814acc3f25bdb906887a2023980d8f49a0b95b",
    strip_prefix = "rules_proto_grpc-4.1.0",
    urls = ["https://github.com/rules-proto-grpc/rules_proto_grpc/archive/4.1.0.tar.gz"],
)

load("@rules_proto_grpc//:repositories.bzl", "rules_proto_grpc_toolchains", "rules_proto_grpc_repos")
rules_proto_grpc_toolchains()
rules_proto_grpc_repos()

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
rules_proto_dependencies()
rules_proto_toolchains()

load("@rules_proto_grpc//js:repositories.bzl", rules_proto_grpc_js_repos = "js_repos")

rules_proto_grpc_js_repos()