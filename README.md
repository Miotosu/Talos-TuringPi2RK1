An ansible playbook for deploying Talos Linux to a Turing Pi 2 cluster with four Turing RK1 modules.

## Update hosts.ini and all.yaml 
Update inventory/hosts.ini and inventory/group_vars/all.yaml for your IP addresses, usernames, passwords, etc.

## Run the full playbook (this WILL erase/flash your Turing Pi modules!):
`ansible-playbook site.yaml -i inventory/hosts.ini --ask-become-pass`

If you must enter a password for sudo, --ask-become-pass will prompt for sudo password at script start.

If you don't need a password for sudo, you can omit the --asl-become-pass argument.

## Skip specific tasks:
 `ansible-playbook site.yaml -i inventory/hosts.ini --ask-become-pass --skip-tags "flash-modules"`

## Run only specific tasks:
`ansible-playbook site.yaml -i inventory/hosts.ini --ask-become-pass --tags "install-tpi,install-talosctl"`

## List of tasks that can be skipped or ran individually/specifically:
- install-tpi - Download and install tpi deb via https://github.com/turing-machines/tpi
- install-talosctl - Download and install talosctl via https://github.com/siderolabs/talos
- download-talos - Download Talos image via https://factory.talos.dev/
- flash-modules - Flash downloaded image to four RK1 nodes in Turing Pi 2
  - flash-module-1 - Flash node 1
  - flash-module-2 - Flash node 2
  - flash-module-3 - Flash node 3
  - flash-module-4 - Flash node 4
- configure-cluster - Generate Talos config (controlplane.yaml, worker.yaml, talosconfig)
- apply-config - Apply the cluster config to the control plane
- configure-talosctl - Bootstrap the cluster and generate kubeconfig
- add-workers - Add worker nodes to the cluster

## Credits:
This was built using JamesTurland's (aka Jim's Garage) Talos ansible playbook as a starting point: https://github.com/JamesTurland/JimsGarage/tree/main/Ansible/Playbooks/Talos

YouTube video walkthrough of that ansible playbook can be found here: https://www.youtube.com/watch?v=TP8hVq1lCxM