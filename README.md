# rule-js-issue-repro


This repo illustrates a bug with `js_image_layer`. The app is essentially a js binary  that contains a rust binary as a data dependency, and the rust binary contains cc library as its dependency.

When running `bazel run //app:image` in this repro, the following error occurs:


```
ERROR: /home/ubuntu/rule-js-issue-repro/app/BUILD:12:15: JsImageLayer //app:layers failed: (Exit 1): js_image_layer_builder.sh failed: error executing command (from target //app:layers) bazel-out/k8-opt-exec-2B5CBBC6-ST-625e526ca8a8/bin/external/aspect_rules_js/js/private/js_image_layer_builder.sh bazel-out/k8-fastbuild-ST-4a519fd6d3e4/bin/app/layers_entries.json ... (remaining 3 arguments skipped)

Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging
file:///home/ubuntu/.cache/bazel/_bazel_ubuntu/a7fa0a4645cd94ef55cf50ea86708937/sandbox/linux-sandbox/1/execroot/test/bazel-out/k8-opt-exec-2B5CBBC6-ST-625e526ca8a8/bin/external/aspect_rules_js/js/private/js_image_layer_builder.sh.runfiles/aspect_rules_js/js/private/js_image_layer.mjs:9581
    throw new Error(`couldn't map ${value} to a path. please file a bug at https://github.com/aspect-build/rules_js/issues/new/choose`);
          ^

Error: couldn't map bazel-out/k8-fastbuild-ST-4a519fd6d3e4/bin/dep/libc_main.so to a path. please file a bug at https://github.com/aspect-build/rules_js/issues/new/choose
    at findKeyByValue (file:///home/ubuntu/.cache/bazel/_bazel_ubuntu/a7fa0a4645cd94ef55cf50ea86708937/sandbox/linux-sandbox/1/execroot/test/bazel-out/k8-opt-exec-2B5CBBC6-ST-625e526ca8a8/bin/external/aspect_rules_js/js/private/js_image_layer_builder.sh.runfiles/aspect_rules_js/js/private/js_image_layer.mjs:9581:11)
    at build (file:///home/ubuntu/.cache/bazel/_bazel_ubuntu/a7fa0a4645cd94ef55cf50ea86708937/sandbox/linux-sandbox/1/execroot/test/bazel-out/k8-opt-exec-2B5CBBC6-ST-625e526ca8a8/bin/external/aspect_rules_js/js/private/js_image_layer_builder.sh.runfiles/aspect_rules_js/js/private/js_image_layer.mjs:9730:30)
Target //app:image failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 8.357s, Critical Path: 3.12s
INFO: 3 processes: 3 internal.
FAILED: Build did NOT complete successfully
ERROR: Build failed. Not running target
```
