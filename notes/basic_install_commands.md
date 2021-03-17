sudo parted /dev/nvme0n1 -- mklabel msdos
sudo parted /dev/nvme0n1 -- mkpart primary 1MiB -48GiB
sudo parted /dev/nvme0n1 -- mkpart primary linux-swap -48GiB 100%

sudo mkfs.ext4 -L nixos /dev/nvme0n1p1
sudo mkswap -L swap /dev/nvme0n1p2

sudo mount /dev/disk/by-label/nixos /mnt

sudo swapon /dev/nvme0n1p2

sudo nixos-generate-config --root /mnt

sudo rm /mnt/etc/nixos/configuration.nix
sudo nano /mnt/etc/nixos/configuration.nix

sudo nixos-install
