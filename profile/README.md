# ILP32Wrt

**Router firmware based on *OpenWrt* 25.12 that uses a quarter less memory.**

## Why a router?
On a router, the real work happens in the kernel: routing, NAT, the firewall and Wi-Fi run there,
and the kernel stays a full 64-bit kernel. User space runs the management side, such as LuCI,
DNS, ad blocking and scripts, and on a device with little RAM its main job is to stay small.

ILP32Wrt builds that user space as AArch64 ILP32: 64-bit Arm code with 32-bit pointers
(musl, `aarch64_ilp32`). Every process gets smaller, and user space uses about a quarter less memory.

## What ILP32Wrt adds
- **An ILP32 user land** on a 64-bit kernel with ILP32 support.
- **clang for the busiest packages.** ucode, lucihttp, ucode-mod-html and json-c are built with
  clang 22 and our [patches](https://github.com/ilp32-a64/llvm-ilp32), which keep pointer arithmetic
  32-bit and fold address offsets into the addressing modes. Everything else uses GCC 14.3.

With these packages on the *OpenWrt* One, a firewall reload and LuCI are only about 2% slower than
the same tree built for standard 64-bit (LP64). [Benchmarks](https://ilp32.org/en/benchmarks/)

## Repositories
| Repository | Content |
|---|---|
| [ilp32wrt](https://github.com/ilp32-a64/ilp32wrt) | Build tree, firmware releases and device reports |
| [packages](https://github.com/ilp32wrt/packages) | Fork of the packages feed (`openwrt-25.12`) for ILP32Wrt |
| [luci](https://github.com/ilp32wrt/luci) | Fork of the LuCI feed (`openwrt-25.12`) for ILP32Wrt |

We fork a feed only when we need to change it. Fixes that are not specific to ILP32 go upstream.
The kernel, C libraries and compilers are maintained in [ilp32-a64](https://github.com/ilp32-a64).

## Get Involved
Device reports, issues and pull requests are welcome.

ILP32Wrt is not affiliated with OpenWrt. OpenWrt is a registered trademark owned by Software Freedom
Conservancy (SFC); see [openwrt.org](https://openwrt.org).
