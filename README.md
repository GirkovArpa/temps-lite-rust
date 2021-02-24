# temps-lite (Rust)

Rust port of [temps-lite](https://github.com/girkovarpa/temps-lite).

## Compiling for Linux

Before running `cargo build --release`, please be aware of some Windows-specific things.

- In [main.rs](src/main.rs):

```rust
#![windows_subsystem="windows"]
```

I'm not sure if this is safe to leave or must be commented out or deleted.  It's purpose is to hide the console window.

- In [build.rs](build.rs):

```rust
if cfg!(target_os = "windows") {
Command::new("packfolder")
  .args(&["app", "target/assets.rc", "-binary"])
  .output()
  .expect("Unable to run packfolder.exe!");
  WindowsResource::new()
    .set_icon("icon.ico")
    .compile();
}
```

This way of setting the icon is of course incompatible with Linux.  Also, the call to [packfolder]([packfolder](https://github.com/c-smile/sciter-sdk/blob/master/bin.win/packfolder.exe)).exe should be replaced with the equivalent of calling the [packfolder](https://github.com/c-smile/sciter-sdk/blob/master/bin.lnx/packfolder).