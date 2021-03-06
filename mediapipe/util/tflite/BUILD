# Copyright 2019 The MediaPipe Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

licenses(["notice"])  # Apache 2.0

package(default_visibility = [
    "//mediapipe:__subpackages__",
])

cc_library(
    name = "cpu_op_resolver",
    srcs = ["cpu_op_resolver.cc"],
    hdrs = ["cpu_op_resolver.h"],
    deps = [
        "//mediapipe/util/tflite/operations:max_pool_argmax",
        "//mediapipe/util/tflite/operations:max_unpooling",
        "//mediapipe/util/tflite/operations:transpose_conv_bias",
        "@org_tensorflow//tensorflow/lite:builtin_op_data",
        "@org_tensorflow//tensorflow/lite/kernels:builtin_ops",
    ],
)

cc_library(
    name = "op_resolver",
    srcs = ["op_resolver.cc"],
    hdrs = ["op_resolver.h"],
    deps = [
        "@org_tensorflow//tensorflow/lite:builtin_op_data",
        "@org_tensorflow//tensorflow/lite/kernels:builtin_ops",
    ],
)

cc_library(
    name = "tensor_buffer",
    srcs = ["tensor_buffer.cc"],
    hdrs = ["tensor_buffer.h"],
    deps = [
        "@org_tensorflow//tensorflow/lite:framework",
        "@com_google_absl//absl/memory",
        "//mediapipe/framework:port",
    ] + select({
        "//mediapipe/gpu:disable_gpu": [],
        "//mediapipe:ios": [
            "//mediapipe/gpu:MPPMetalUtil",
            "//mediapipe/gpu:gl_base",
        ],
        "//conditions:default": [
            "@org_tensorflow//tensorflow/lite/delegates/gpu/gl:gl_buffer",
            "//mediapipe/gpu:gl_base",
            "//mediapipe/gpu:gl_context",
        ],
    }),
)

cc_test(
    name = "tensor_buffer_test",
    srcs = ["tensor_buffer_test.cc"],
    deps = [
        ":tensor_buffer",
        "//mediapipe/framework/port:gtest_main",
    ] + select({
        "//mediapipe/gpu:disable_gpu": [],
        "//conditions:default": [],
    }),
)
