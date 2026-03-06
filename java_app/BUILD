package(default_visibility = ["//visibility:public"]) 

java_library(
    name = "lib",
    srcs = ["src/main/java/com/example/App.java"],
)

java_binary(
    name = "app",
    main_class = "com.example.App",
    runtime_deps = [":lib"],
)

java_test(
    name = "AppTestNg",
    srcs = ["src/test/java/com/example/AppTestNg.java"],
    deps = [
        ":lib",
        "@maven//:org_testng_testng",
    ],
    use_testrunner = False,
    main_class = "org.testng.TestNG",
    args = ["-testclass", "com.example.AppTestNg"],
)
