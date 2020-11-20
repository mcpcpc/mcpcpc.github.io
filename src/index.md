# mcpcpc.com

My name is Michael Czigler and I create minimum viable solutions written in the C programming language.

## xwm

[xwm](https://github.com/mcpcpc/xwm) ("XCB Window Manager") is a tiny floating 
window manager written using the XCB protocol. This project provides a limited 
set of out-of-box features:

* Parameterized window settings (default sizes, borders, colors, etc.).
* Configurable and extendable key bindings and default utilities (`st`, 
  `dmenu`, `surf`, etc.).
* POSIX C99 and MISRA-C compliant, which  promotes portability, security and 
  safety of the source.

This sets the expectation for the the user to expand or patch features that they
so desire. For patch examples (and screenshots of xwm in use), refer to the
[xwm-patches](http://github.com/mcpcpc/xwm-patches) repository.

The acyronym `xwm` is a homage to the original and now-defunct "X Window Manager". 
Both projects are unaffiliated and do not share any common source code.

To get started, one can simply use `git` and `make` commands to build and install
`xwm`:

```shell
git clone https://github.com/mcpcpc/xwm
cd xwm
make
sudo make install
```

## xbg

[xbg](https://github.com/mcpcpc/xbg) is a tiny background color setter written 
using the XCB protocol. 

To get started, one can simply use `git` and `make` commands to build and install 
`xbg`:

```shell
git clone https://github.com/mcpcpc/xbg
cd xbg
make
sudo make install
```

Once installed, setting a new background is a simple as specify the the X11 color name as an argument from any virtual terminal emulator:

```shell
xbg teal
```

## μss

μss ("Micro Static Site") is a static-site generator designed for small 
hosting platforms. This project is currently a work in-progress and is 
intended to replace the current generator for this page.

---

Questions? Send mail to info[at]mcpcpc[dot]com or one of the following:

| [reddit](https://www.reddit.com/user/mcpcpc) | [github](https://github.com/mcpcpc) |
| ------ | ------ |
