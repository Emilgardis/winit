# gl-init-rs

Alternative to GLFW in pure Rust.

## Try it!

```
git clone https://github.com/tomaka/gl-init-rs
cd gl-init-rs
cargo test
./target/test/window    // or target\test\window.exe
```

## Usage

```rust
extern crate init = "gl-init-rs";
extern crate libc;
extern crate gl;

fn main() {
    use std::default::Default;

    let window = init::Window::new().unwrap();

    unsafe { window.make_current() };

    gl::load_with(|symbol| window.get_proc_address(symbol) as *const libc::c_void);

    gl::ClearColor(0.0, 1.0, 0.0, 1.0);

    while !window.should_close() {
        window.wait_events();

        gl::Clear(gl::COLOR_BUFFER_BIT);

        window.swap_buffers();
    }
}
```
