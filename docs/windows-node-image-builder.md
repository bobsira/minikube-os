# Windows Node Image Builder

## Prerequisites

- Make sure the Hyper-V role is enabled
- Install the Windows Assessment and Deployment Kit (32-bit version). <https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install#download-the-adk-for-windows-11-version-22h2>
- Add the following location the the system path variable: C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\x86\Oscdimg

### On Powershell Administrator complete the following steps

1. Clone the repo

```powershell
git clone --branch feature/windows-node-image-builder https://github.com/kubernetes-sigs/minikube-os.git
```

2. Change the current directory to the deploy folder and then the Windows image builder:

```powershell
cd deploy\windows-node-image
```

3. Install packer using the command below

```powershell
choco install packer
```

4. Then run the following commands:

```powershell
packer -v 
packer plugins install github.com/hashicorp/hyperv
packer init windows.json.pkr.hcl
packer fmt --var-file=./windows.auto.pkrvars.hcl windows.json.pkr.hcl
packer validate .
packer build -force -var-file="windows.auto.pkrvars.hcl" "windows.json.pkr.hcl"
```

To override versions locally:
Add -var 'windows_version=2022' -var 'kubernetes_version=v1.35.0' -var 'containerd_version=1.7.25' (or your desired values) to your Packer commands:

```powershell
packer build -force -var-file="windows.auto.pkrvars.hcl" -var 'windows_version=2022' -var 'kubernetes_version=v1.35.0' -var 'containerd_version=1.7.25' "windows.json.pkr.hcl"
```

### Default password

|OS|username|password|
|--|--------|--------|
|Windows|Administrator|password|
