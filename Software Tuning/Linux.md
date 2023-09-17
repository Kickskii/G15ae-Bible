# Introduction

# Arch 

## Instalacion 

Requisitos en el Bios
	nvme raid off, secure boot off
Particionar los 2 discos duros
	Mostrar discos: `fdisk -l`
	Disco 1  `cfdisk /dev/nvme0n1` (Usar GPT)
		boot create 500M
		swap Create 2G
		root Create 115G
	Disco 2 `cfdisk /dev/nvme1n1` (Usar GPT)
		EFI Create 500M
		swap Create 2G
		root Create 115G
	Verificar discos `gdisk /dev/nvmexnx -p` 
Hacer swap (asumiendo que la partición 2 es el swap)
	`mkswap /dev/nvme0n1p2`
	`mkswap /dev/nvme1n1p2`
	Prender el swap `swapon /dev/nvme[0-1]n1p2`
	Confirmación del swap "lsblk"
Creacion de un MD RAID 0
	Creación del disco raid (3 siendo la particion de 115GB)
		`mdadm --create /dev/md0 --chunk=128K --level=0 --raid-devices=2 /dev/nvme0n1px  /dev/nvme1n1p`
	Checar si se hizo adecuadamente: `cat /proc/mdstat` 
	Utilizar lvm para hacer el volumen
		`pvcreate /dev/md0`
		`vgcreate volgrp1 /dev/md0`
		`lvcreate -L 230GiB -n pool volgrp1`
	Formatear y montar para instalacion
		`mkfs.f2fs /dev/volgrp1/pool`
		`mount /dev/volgrp1/pool /mnt`
Instalacion de arch
	Montar particion boot 
		`mount /dev/nvme1n1p1 /mnt/boot`
	Guardar Espejos  a pacman
		`reflector -c US -c UK -a 12 -p https --sort rate --save /etc/pacman.d/mirrorlist`
	Instalacion base
		`pacstrap /mnt base base-devel linux linux-firmware linux-headers nano amd-ucode reflector mtools dosfstools mdadm lvm2 f2fs-tools`
	Generacion de fstab
		`genfstab -U /mnt >> /mnt/etc/fstab`
	Chroot 
		`arch-chroot /mnt`
			Ajustar la fecha y hora
				`ln -sf /usr/share/zoneinfo/America/Your country/etc/localtime`
				`hwclock --systohc`
			Ajustar Idioma
				en `nano /etc/locale.gen` y quitar el # de `#en_US.UTF-8 UTF-8`
			Generar Locale
				`locale-gen`
				adicionar el idioma
				 `echo LANG=en_US.UTF-8 > /etc/locale.conf` 
			Escoger idioma del teclado
				`echo "KEYMAP=US" > /etc/vconsole.conf`
			Escoger nombre
				`echo NAME > /etc/hostname`
			Crear Hosts
				en `nano /etc/hosts` escribir 
				```127.0.0.1    localhost
				::1          localhost
				127.0.1.1    NAME.localdomain NAME```
			Instalar el administrador de redes
				`pacman -S networkmanager`
				Montar el servicio 
					`systemctl enable NetworkManager`
			Establecer contrase;a
				`passwd`
			Configurar Systemd Boot
				`bootctl --path=/boot install`
				Crear archivo de configuracion para el booteo
					`touch /boot/loader/entries/arch.conf`
					abrir con nano
						`nano -w /boot/loader/entries/arch.conf`
					Escribir
						```title Arch Linux
						linux /vmlinuz-linux
						initrd /initramfs-linux.img
						options root=/dev/volgrp1/pool rw```
				Configurar las opciones de `loader.conf`
					Escribir en `loader.conf` 
						`nano -w /boot/loader/loader.conf`
							`timeout 4`
							`console-mode max`
							`editor no`
				Actualizar `Systemd-boot`
					`bootctl --path=/boot update`
			Configurar `mkinitcpio.conf`
				Escribir en `mkinitcpio.conf`
					`nano /etc/mkinitcpio.conf`
						`MODULES=(dm-raid raid0)``
						`HOOKS=(base systemd ... block mdadm_udev lvm2 filesystems fsck)`
						siendo ... lo que esta despues de systemd
		`exit`
	Desmontar 
		`umount -a`
	Reiniciar
		`reboot` 
Post Instalacion


## Funcionalidad 
Perfiles de energia
	Perfil ultrabajo de energia, no tengo idea
	Perfil ahorrador
		Buscar como hacer una notificacion o algun iconoi
			`sudo cpupower frequency-set -g powersave`
			Buscar una curva de ventilador 
	Perfil rendimiento
		`sudo cpupower frequency-set -g performance`
		Buscar curva de ventilador
		buscar hacer una notificacion
	To set a preference, run the following command with the desired preference:
	`echo power | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/energy_performance_preference`
	Available preferences: `performance`, `power`, `balance_power`, `balance_performance`
	https://lore.kernel.org/lkml/20221219064042.661122-1-perry.yuan@amd.com/

Monitores de recursos
Frecuencia de audifonos
Bug de tpm
Gestos con el touchpad
	Scroll de 3 dedos
touchpad de precision

UMAF
	Hibernar a ram s3


Herramientas de powertoys

Mejorar la calidad y el volumen de las bocinas, con equalizador
Btop mostrar gpu
Hacer que Dolphin pueda cambiar nombres como Bulk Rename Utility
	Krename
Hacer que Dolphin muestre carpetas por tamaño
Hacer que Dolphin pueda hacer divisiones de muchas carpetas como Folder axe
Hacer que Dolphin pueda administrar archivos como Bulk File Manager
Hacer que Dolphin pueda copiar archivos como smart copy
Hacer que Dolphin pueda comparar archivos como BeyondCompare
	Kompare
Krusader??

## Problemas
Caracteres que no son utf-8 como japoneses
	Se soluciona instalando noto algo
rog control center
	es necesario?
si kde se jode es por ver muchos caracteres?
borrar screenmapping ~/.config/plasma-org.kde.plasma.desktop-appletsrc
firefox crashea 

## Seguridad
Sandbox de firefox

## Velocidad
Undervolt
Kernel
	Cachy-OS (tecnicamente con esto no requiero autocpufreq, tlp no c)
Compilacion
	Paru
Compilar todo
	PGO y BOLT
	https://github.com/CachyOS/linux-cachyos
https://gitlab.com/ananicy-cpp/ananicy-cpp
	
## Temp
Mkinicpio
	MODULES=(amdgpu)
	BINARIES=()
	FILES=()
	HOOKS=(systemd autodetect keyboard sd-vconsole modconf block filesystems fsck)
arch.conf
	title Arch Linux (linux-zen)
	linux /vmlinuz-linux-zen
	initrd /amd-ucode.img
	initrd /initramfs-linux-zen.img
	options root=PARTUUID=a00914fa-2109-4e3a-a227-40622aca1473 rw rootfstype=f2fs quiet loglevel=3 systemd.show_status=auto rd.udev.log_level=3 nowatchdog mitigations=off vt.global_cursor_default=0 iommu=pt clocksource=tsc tsc=reliable
	}} Error potencial tsc=unstable trace_clock=local
etc / makepkg.conf
	CARCH="x86_64"
	CHOST="x86_64-pc-linux-gnu"
	#-- Compiler and Linker Flags
	#CPPFLAGS=""
	CFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fno-plt -fexceptions \
	        -Wp,-D_FORTIFY_SOURCE=2 -Wformat -Werror=format-security \
	        -fstack-clash-protection -fcf-protection"
	CXXFLAGS="$CFLAGS -Wp,-D_GLIBCXX_ASSERTIONS"
	LDFLAGS="-Wl,-O1,--sort-common,--as-needed,-z,relro,-z,now"
	LTOFLAGS="-flto=auto"
	#RUSTFLAGS="-C opt-level=2"
	#-- Make Flags: change this for DistCC/SMP systems
	#MAKEFLAGS="-j2"
	#-- Debugging flags
	DEBUG_CFLAGS="-g"
	DEBUG_CXXFLAGS="$DEBUG_CFLAGS"
	#DEBUG_RUSTFLAGS="-C debuginfo=2"
https://github.com/codeswhite/kzones
https://github.com/Bismuth-Forge/bismuth
https://wiki.archlinux.org/title/list_of_applications#top-page
https://github.com/fhanau/Efficient-Compression-Tool


