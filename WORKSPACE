workspace(name = "bzlmod_ws_dual")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# --- rules_jvm_external (WORKSPACE mode) ---
RULES_JVM_EXTERNAL_TAG = "6.6"
RULES_JVM_EXTERNAL_SHA = "3afe5195069bd379373528899c03a3072f568d33bd96fe037bd43b1f590535e7"

http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    urls = [
        "https://github.com/bazel-contrib/rules_jvm_external/releases/download/%s/rules_jvm_external-%s.tar.gz"
        % (RULES_JVM_EXTERNAL_TAG, RULES_JVM_EXTERNAL_TAG),
    ],
)

load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")
rules_jvm_external_deps()

load("@rules_jvm_external//:setup.bzl", "rules_jvm_external_setup")
rules_jvm_external_setup()

load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    name = "maven",
    artifacts = [
        "org.testng:testng:7.12.0",
    ],
    repositories = [
        "https://repo1.maven.org/maven2",
    ],
    # After pinning:
    # maven_install_json = "//:maven_install.json",
)

# --- C++ external deps (WORKSPACE mode) ---

# GoogleTest (matches Bzlmod repo name)
http_archive(
    name = "googletest",
    urls = ["https://github.com/google/googletest/archive/refs/tags/v1.15.2.zip"],
    strip_prefix = "googletest-1.15.2",
)

# nlohmann_json (header‑only)
http_archive(
    name = "nlohmann_json",
    urls = ["https://github.com/nlohmann/json/archive/refs/tags/v3.12.0.zip"],
    strip_prefix = "json-3.12.0",
    build_file_content = """
package(default_visibility=["//visibility:public"])

filegroup(
    name = "headers",
    srcs = glob(["single_include/**/*.hpp", "single_include/**/*.h"]),
)

cc_library(
    name = "json",
    hdrs = [":headers"],
    includes = ["single_include"],
)
""",
)
