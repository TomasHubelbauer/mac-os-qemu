# macOS in Qemu

A collection of links relating installing and running macOS in Qemu.

## On Arch

https://passthroughpo.st/new-and-improved-mac-os-tutorial-part-1-the-basics/

This would require me to run Arch on real hardware, probably.
It also has Debian thingies but meh.

## On Windows

In theory all of the above should be portable to Windows?

This is the real meat: https://github.com/foxlet/macOS-Simple-KVM

I started porting it in https://github.com/TomasHubelbauer/sus-downloader
Now I am able to download macOS packages from SUS but it remains to be seen if DMG2IMG will work on Windows
or will be runnable in WSL or something like that and if the Qemu switchers in that repository will work on
Windows.

Turns out `dmg2img` has a Windows build and it works alright. The Qemu switches almost worked, I just had to
switch `vga` to `virtio` and to remove `+aex` from the CPU extensions. Also had to get rid of any KVM related
acceleration thingies. The IMG format had to be explicitly set to `raw` to dismiss a warning, which I don't
think is Windows specific, so I think I am just using a newer version of Qemu which adds it.

Right now attempting the install to see where that goes.

```
qemu-system-x86_64
  -m 2G
  -machine q35
  -smp 4,cores=2 -cpu Penryn,vendor=GenuineIntel,kvm=on,+sse3,+sse4.2,+xsave,+avx,+xsaveopt,+xsavec,+xgetbv1,+avx2,+bmi2,+smep,+bmi1,+fma,+movbe,+invtsc
  -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
  -smbios type=2
  -drive if=pflash,format=raw,readonly,file=OVMF_CODE.fd
  -drive if=pflash,format=raw,file=OVMF_VARS.fd
  -vga virtio
  -device ich9-intel-hda
  -device hda-output
  -usb
  -device usb-kbd
  -device usb-tablet
  -netdev user,id=net0
  -device e1000-82545em,netdev=net0,id=net0,mac=52:54:00:c9:18:27
  -device ich9-ahci,id=sata
  -drive id=ESP,if=none,format=qcow2,file=ESP.qcow2
  -device ide-hd,bus=sata.2,drive=ESP
  -drive id=InstallMedia,if=none,file=BaseSystem.img,format=raw
  -device ide-hd,bus=sata.3,drive=InstallMedia
```

## Dean Ends

https://github.com/kholia/OSX-KVM dissed in https://passthroughpo.st/an-open-letter-to-linus-tech-tips-and-a-psa/
