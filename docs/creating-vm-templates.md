wget <https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img>

qm create 8001 --memory 2048 --core 2 --name ubuntu-cloud --net0 virtio,bridge=vmbr0
qm importdisk 8001 jammy-server-cloudimg-amd64.img local-lvm
qm set 8001 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-8001-disk-0
qm set 8001 --ide2 local-lvm:cloudinit
qm set 8001 --boot c --bootdisk scsi0
qm set 8001 --serial0 socket --vga serial0
qm template 8001

qm clone 8001 503 --name k3s-controller-2 --full
qm clone 8002 605 --name k3s-worker-5 --full
qm clone 8002 606 --name k3s-worker-6  --full
qm clone 8002 607 --name k3s-worker-7  --full
