# Starting to Shape the custom release

After cloning your custom repository and after you cd  into it, you would face a profile which later makes parch happens.

## Naming the release

Open profiledef file that is placed inside the iso directory, to set the name of release, the content should be like this:

```
#!/usr/bin/env bash
# shellcheck disable=SC2034

iso_name="Parchlinux"
iso_label="PARCH_LINUX$(date +%Y%m)"
iso_publisher="Parch Linux<https://parchlinux.com>"
iso_application="Parch Linux Live/Rescue CD"
iso_version="$(date +%Y.%m.%d)"
install_dir="arch"
buildmodes=('iso')
bootmodes=('bios.syslinux.mbr' 'bios.syslinux.eltorito'
           'uefi-ia32.grub.esp' 'uefi-x64.systemd-boot.esp'
           'uefi-ia32.grub.eltorito' 'uefi-x64.systemd-boot.eltorito')
arch="x86_64"
pacman_conf="pacman.conf"
airootfs_image_type="squashfs"
airootfs_image_tool_options=('-comp' 'xz' '-Xbcj' 'x86')
file_permissions=(
  ["/etc/shadow"]="0:0:400"
  ["/root"]="0:0:750"
  ["/root/.automated_script.sh"]="0:0:755"
  ["/usr/local/bin/choose-mirror"]="0:0:755"
  ["/usr/local/bin/Installation_guide"]="0:0:755"
  ["/usr/local/bin/livecd-sound"]="0:0:755"
)

```

you can change the iso_name to your desigerd name for example: Parch Linux Designer Edition

and the iso lable is what the iso shows after get mounted or written to a usb disk, cd or etc...

dont touch other things, save the file and exit after changing the name and lable.

## Adding packages to the release

For adding packages you need to edit the packages.x86_64 file located in iso directory. write the name of your packages there and save it.

**Note**

Its better to use ```#lables``` to set the packages lables and grouping them.


## Display Manager

All versions of parchlinux expect gnome, uses SDDM as the default display manager, the sddm is predefined inside the packages file and pre-enabled by default inside the Systemd services.

### Changing the theme for SDDM

simply just ask the developers to package your theme and put them inside PCP mirror, then make a theme.conf file inside the iso/airootfs/etc/sddm.conf.d/ and set the theme name and cursor theme name there.


### Autologin file

Remember to edit the autologin file located inside iso/airootfs/etc/sddm.conf.d and set the proper desktop name for it, if you dont after booting you would see the login screen


## Adding Dotfiles

You can add your dotfiles for DE or Applications inside iso/airootfs/etc/skel or just ask a Repo Maintainer to package them for you and put them inside the pcp repository.

## Installer

Parch by default uses calamares and that is recommended to put **calamares** and **calamares-parch** packages inside your package list.

**Note**

Do not edit or remove parchlinux core packages inside the packages file, you would get a unbootable iso image.

## Kernel

Currently the only kernel which is supported by live iso is the generic kernel. please dont use zen or xanmod or you would get a unbootable image.

# Testing changes

You can test your changes by running the build.sh file, it would make a iso for you.
