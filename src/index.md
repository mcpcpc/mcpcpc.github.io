# mcpcpc.com 

My name is Michael Czigler and I create minimally viable solutions written in C.

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
using the XCB protocol. Using this project is intended to be a straight forward
as possible and executable through any virtual terminal.

To get started, one can simply use `git` and `make` commands to build and install 
`xbg`:

```shell
git clone https://github.com/mcpcpc/xbg
cd xbg
make
sudo make install
```

---

Questions? Feel free to reach out to me via email at info[at]mcpcpc[dot]com,
Freenode IRC channels [#kisslinux](https://freenode.logbot.info/kisslinux) and
[#kirc](https://freenode.logbot.info/kirc), or on
[reddit](https://www.reddit.com/user/mcpcpc).
