# macOS in Qemu

A collection of links relating installing and running macOS in Qemu.

## On Arch

https://passthroughpo.st/new-and-improved-mac-os-tutorial-part-1-the-basics/

This would require me to run Arch on real hardware, probably.
It also has Debian thingies but meh.

## On Windows

In theory all of the above should be portable to Windows?

This is the real meat: https://github.com/foxlet/macOS-Simple-KVM
It downloads macOS from Apple servers (a portable / directly runnable Python script),
then uses `dmgtoimg` (which is in the repository as a binary not source - ???)
and then wraps a few Qemu switches in a Bash script which should also be portable
assuming Qemu switches are stable across Linux and Windows.

## Dean Ends

https://github.com/kholia/OSX-KVM dissed in https://passthroughpo.st/an-open-letter-to-linus-tech-tips-and-a-psa/
