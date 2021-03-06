load("@org_tensorflow//third_party/mlir:tblgen.bzl", "gentbl")

licenses(["notice"])

package(default_visibility = [":test_friends"])

# Please only depend on this from MLIR tests.
package_group(
    name = "test_friends",
    packages = ["//..."],
)

cc_library(
    name = "IRProducingAPITest",
    hdrs = ["APITest.h"],
    includes = ["."],
)

gentbl(
    name = "TestLinalgTransformPatternsIncGen",
    tbl_outs = [
        (
            "-gen-rewriters",
            "lib/DeclarativeTransforms/TestLinalgTransformPatterns.h.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "lib/DeclarativeTransforms/TestLinalgTransformPatterns.td",
    td_srcs = [
        "@llvm-project//mlir:LinalgTransformPatternsTdFiles",
    ],
)

gentbl(
    name = "TestVectorTransformPatternsIncGen",
    tbl_outs = [
        (
            "-gen-rewriters",
            "lib/DeclarativeTransforms/TestVectorTransformPatterns.h.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "lib/DeclarativeTransforms/TestVectorTransformPatterns.td",
    td_srcs = [
        "@llvm-project//mlir:VectorTransformPatternsTdFiles",
    ],
)

gentbl(
    name = "TestOpsIncGen",
    strip_include_prefix = "lib/TestDialect",
    tbl_outs = [
        (
            "-gen-op-decls",
            "lib/TestDialect/TestOps.h.inc",
        ),
        (
            "-gen-op-defs",
            "lib/TestDialect/TestOps.cpp.inc",
        ),
        (
            "-gen-dialect-decls",
            "lib/TestDialect/TestOpsDialect.h.inc",
        ),
        (
            "-gen-enum-decls",
            "lib/TestDialect/TestOpEnums.h.inc",
        ),
        (
            "-gen-enum-defs",
            "lib/TestDialect/TestOpEnums.cpp.inc",
        ),
        (
            "-gen-rewriters",
            "lib/TestDialect/TestPatterns.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "lib/TestDialect/TestOps.td",
    td_srcs = [
        "@llvm-project//mlir:OpBaseTdFiles",
        "@llvm-project//mlir:include/mlir/IR/OpAsmInterface.td",
        "@llvm-project//mlir:include/mlir/Interfaces/CallInterfaces.td",
        "@llvm-project//mlir:include/mlir/Interfaces/ControlFlowInterfaces.td",
        "@llvm-project//mlir:include/mlir/Interfaces/InferTypeOpInterface.td",
        "@llvm-project//mlir:include/mlir/Interfaces/SideEffects.td",
    ],
    test = True,
)

cc_library(
    name = "TestDialect",
    srcs = [
        "lib/TestDialect/TestDialect.cpp",
        "lib/TestDialect/TestPatterns.cpp",
    ],
    hdrs = [
        "lib/TestDialect/TestDialect.h",
    ],
    includes = [
        "lib/DeclarativeTransforms",
        "lib/TestDialect",
    ],
    deps = [
        ":TestOpsIncGen",
        "@llvm-project//llvm:support",
        "@llvm-project//mlir:ControlFlowInterfaces",
        "@llvm-project//mlir:Dialect",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:InferTypeOpInterface",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:SideEffects",
        "@llvm-project//mlir:StandardOps",
        "@llvm-project//mlir:TransformUtils",
        "@llvm-project//mlir:Transforms",
    ],
)

cc_library(
    name = "TestIR",
    srcs = [
        "lib/IR/TestFunc.cpp",
        "lib/IR/TestMatchers.cpp",
        "lib/IR/TestSideEffects.cpp",
        "lib/IR/TestSymbolUses.cpp",
    ],
    deps = [
        ":TestDialect",
        "@llvm-project//llvm:support",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:StandardOps",
        "@llvm-project//mlir:Support",
    ],
)

cc_library(
    name = "TestPass",
    srcs = [
        "lib/Pass/TestPassManager.cpp",
    ],
    deps = [
        "@llvm-project//llvm:support",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:Support",
    ],
)

cc_library(
    name = "TestTransforms",
    srcs = glob([
        "lib/Transforms/*.cpp",
    ]),
    includes = ["lib/TestDialect"],
    deps = [
        ":TestDialect",
        ":TestLinalgTransformPatternsIncGen",
        ":TestVectorTransformPatternsIncGen",
        "@llvm-project//llvm:support",
        "@llvm-project//mlir:AffineOps",
        "@llvm-project//mlir:Analysis",
        "@llvm-project//mlir:EDSC",
        "@llvm-project//mlir:GPUDialect",
        "@llvm-project//mlir:GPUTransforms",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:LinalgOps",
        "@llvm-project//mlir:LinalgTransforms",
        "@llvm-project//mlir:LoopOps",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:StandardOps",
        "@llvm-project//mlir:Support",
        "@llvm-project//mlir:TransformUtils",
        "@llvm-project//mlir:Transforms",
        "@llvm-project//mlir:VectorOps",
        "@llvm-project//mlir:VectorToLLVM",
        "@llvm-project//mlir:VectorToLoops",
    ],
)

cc_library(
    name = "TestSPIRV",
    srcs = glob([
        "lib/Dialect/SPIRV/*.cpp",
    ]),
    deps = [
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:Pass",
        "@llvm-project//mlir:SPIRVDialect",
        "@llvm-project//mlir:SPIRVLowering",
    ],
)
