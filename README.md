# Dual‑mode Bazel 7.2.0 (Bzlmod + WORKSPACE)

Languages:
- Java app + TestNG (via Maven)
- C++ app + external deps: GoogleTest + nlohmann_json

## Modes
- **WORKSPACE (default)**: `.bazelrc` disables Bzlmod by default.
- **Bzlmod**: pass `--config=bzlmod`.

## Build / Test
```bash
# WORKSPACE mode
bazel build //:all_apps
bazel test  //:all_tests

# Bzlmod mode
bazel build --config=bzlmod //:all_apps
bazel test  --config=bzlmod //:all_tests
```

## Pin Maven deps (optional but recommended)
```bash
# WORKSPACE mode
bazel run @maven//:pin
# then open WORKSPACE and uncomment maven_install_json line

# Bzlmod mode
bazel run --config=bzlmod @maven//:pin
# then open MODULE.bazel and uncomment lock_file line
```
