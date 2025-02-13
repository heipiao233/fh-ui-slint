# FH-UI for Slint
This is a third-party [Slint](https://slint.dev/) style that "clones" [FH-UI (Simplified Chinese page)](https://sheep-realms.github.io/Fallen-Homes-UI-in-Upperworld/design.html).

> **FH-UI (full name: Fallen Homes UI in Upperworld)** is a front-end framework with a unique style. FH-UI attaches great importance to visual impact, layering and appropriate decoration, and takes liveliness and sharpness as its core design concept. *- Taken from the document.*

Many details of FH-UI are not implemented. Widgets are not tested. Use with caution.

Some source code are copied from Slint source code.

## Usage
1. Use this repo as a submodule called in a seperate directory like `include/fh-ui` in your project and link it to `include/fh-ui-dark` and `include/fh-ui-light`.
```shell
git submodule add https://github.com/heipiao233/fh-ui-slint include/fh-ui
cd include
ln -s fh-ui fh-ui-dark
ln -s fh-ui fh-ui-light
```
2. Add `include` and `include/fh-ui` to your Slint include paths if you use this style. Set style to `fh-ui` (or `fh-ui-dark`/`fh-ui-light`).
```rust
// build.rs
use std::path::PathBuf;

use slint_build::CompilerConfiguration;

fn main() {
    let style = "fh-ui";
    let manifest_dir = PathBuf::from(std::env::var_os("CARGO_MANIFEST_DIR").unwrap());
    let mut conf = CompilerConfiguration::new()
        .with_style(style.into());
    if style.starts_with("fh-ui") {
        conf = conf.with_include_paths(
            vec![manifest_dir.join("include"), manifest_dir.join("include/fh-ui")]);
    }
    slint_build::compile_with_config(
        "ui/app-window.slint",
        conf
    ).expect("Slint build failed");
}
```
```js
import * as slint from "slint-ui";
let style = "fh-ui";
let includePaths = null;
if (style.startsWith("fh-ui")) {
    includePaths = ["include", ""];
}
let ui = slint.loadFile("main.slint", {
    style: "fluent",
    includePaths
});
// Enjoy it.
```
3. Enable SLINT_ENABLE_EXPERIMENTAL_FEATURES in environment vars.
4. Use winit-skia for backend and renderer for best experience.
