sudo parted /dev/nvme0n1 -- mklabel msdos
sudo parted /dev/nvme0n1 -- mkpart primary 1MiB -8GiB
sudo parted /dev/nvme0n1 -- mkpart primary linux-swap -8GiB 100%

sudo mkfs.ext4 -L nixos /dev/nvme0n1p1
sudo mkswap -L swap /dev/nvme0n1p2

sudo mount /dev/disk/by-label/nixos /mnt

sudo mkdir -p /mnt/boot
sudo mount /dev/disk/by-label/boot /mnt/boot

sudo swapon /dev/sda2

sudo nixos-generate-config --root /mnt

sudo rm /mnt/etc/nixos/configuration.nix
sudo nano /mnt/etc/nixos/configuration.nix

sudo nixos-install
