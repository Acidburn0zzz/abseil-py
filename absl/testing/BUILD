licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

config_setting(
    name = "osx",
    constraint_values = ["//third_party/bazel_platforms/os:osx"],
)

config_setting(
    name = "ios",
    flag_values = {"//tools/cpp:cc_target_os": "apple"},
)

_absl_test_platform_deps = select({
    ":osx": [],
    ":ios": [],
    # TODO(b/75911467): Remove after :osx works in host mode
    "//tools/cc_target_os:platform_macos": [],
    "//conditions:default": [
        "//third_party/py/faulthandler",
        "//third_party/py/readline",  # Enables arrow keys and tab-completion in (pdb).
    ],
})

py_library(
    name = "absltest",
    srcs = ["absltest.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":_pretty_print_reporter",
        ":xml_reporter",
        "//absl:_collections_abc",
        "//absl:_enum_module",
        "//absl:app",
        "//absl/flags",
        "//absl/logging",
        "//absl/third_party/unittest3_backport",
        "@six_archive//:six",
    ],
)

py_library(
    name = "flagsaver",
    srcs = ["flagsaver.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        "//absl/flags",
    ],
)

py_library(
    name = "parameterized",
    srcs = [
        "parameterized.py",
    ] + select({
        "//absl:py2_mode": [],
        "//absl:py3_mode": ["_parameterized_async.py"],
    }),
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":absltest",
        "//absl:_collections_abc",
        "@six_archive//:six",
    ],
)

py_library(
    name = "xml_reporter",
    srcs = ["xml_reporter.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":_pretty_print_reporter",
        "//absl/third_party/unittest3_backport",
        "@six_archive//:six",
    ],
)

py_library(
    name = "_bazelize_command",
    testonly = 1,
    srcs = ["_bazelize_command.py"],
    srcs_version = "PY2AND3",
    visibility = ["//:__subpackages__"],
    deps = [
        "//absl/flags",
    ],
)

py_library(
    name = "_pretty_print_reporter",
    srcs = ["_pretty_print_reporter.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//absl/third_party/unittest3_backport",
    ],
)

py_test(
    name = "tests/absltest_filtering_test",
    size = "small",
    srcs = ["tests/absltest_filtering_test.py"],
    data = [":tests/absltest_filtering_test_helper"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":_bazelize_command",
        ":absltest",
        ":parameterized",
        "//absl/logging",
    ],
)

py_binary(
    name = "tests/absltest_filtering_test_helper",
    testonly = 1,
    srcs = ["tests/absltest_filtering_test_helper.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [":absltest"],
)

py_test(
    name = "tests/absltest_fail_fast_test",
    size = "small",
    srcs = ["tests/absltest_fail_fast_test.py"],
    data = [":tests/absltest_fail_fast_test_helper"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":_bazelize_command",
        ":absltest",
        "//absl/logging",
    ],
)

py_binary(
    name = "tests/absltest_fail_fast_test_helper",
    testonly = 1,
    srcs = ["tests/absltest_fail_fast_test_helper.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [":absltest"],
)

py_test(
    name = "tests/absltest_randomization_test",
    size = "medium",
    srcs = ["tests/absltest_randomization_test.py"],
    data = [":tests/absltest_randomization_testcase"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":_bazelize_command",
        ":absltest",
        ":parameterized",
        "//absl/flags",
    ],
)

py_binary(
    name = "tests/absltest_randomization_testcase",
    testonly = 1,
    srcs = ["tests/absltest_randomization_testcase.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":absltest",
    ],
)

py_test(
    name = "tests/absltest_sharding_test",
    size = "small",
    srcs = ["tests/absltest_sharding_test.py"],
    data = [":tests/absltest_sharding_test_helper"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":_bazelize_command",
        ":absltest",
        "//absl/flags",
    ],
)

py_binary(
    name = "tests/absltest_sharding_test_helper",
    testonly = 1,
    srcs = ["tests/absltest_sharding_test_helper.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [":absltest"],
)

py_test(
    name = "tests/absltest_test",
    size = "small",
    srcs = ["tests/absltest_test.py"],
    data = [":tests/absltest_test_helper"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":_bazelize_command",
        ":absltest",
        ":parameterized",
        "//absl/flags",
        "@six_archive//:six",
    ],
)

py_binary(
    name = "tests/absltest_test_helper",
    testonly = 1,
    srcs = ["tests/absltest_test_helper.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":absltest",
        "//absl/flags",
    ],
)

py_test(
    name = "tests/flagsaver_test",
    srcs = ["tests/flagsaver_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":absltest",
        ":flagsaver",
        "//absl/flags",
    ],
)

py_test(
    name = "tests/parameterized_test",
    srcs = ["tests/parameterized_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":absltest",
        ":parameterized",
        "//absl:_collections_abc",
        "@six_archive//:six",
    ],
)

py_test(
    name = "tests/xml_reporter_test",
    srcs = ["tests/xml_reporter_test.py"],
    data = [":tests/xml_reporter_helper_test"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":_bazelize_command",
        ":absltest",
        ":parameterized",
        ":xml_reporter",
        "//absl/logging",
        "//absl/third_party/unittest3_backport",
        "@mock_archive//:mock",
        "@six_archive//:six",
    ],
)

py_binary(
    name = "tests/xml_reporter_helper_test",
    testonly = 1,
    srcs = ["tests/xml_reporter_helper_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":absltest",
        "//absl/flags",
    ],
)
