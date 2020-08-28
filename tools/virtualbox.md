---
description: Setting up new virtual machine.
---

# Virtualbox

## To install Virtualbox

```text
$ sudo apt install virtualbox
```

## To install Virtualbox Extension Pack:

```text
$ sudo apt install virtualbox-ext-pack
```

## To get list of OSs VirtualBox supports:

```text
$ VBoxManage list ostype
```

## To instantiate new VM:

```text
$ VBoxManage createvm --name test --ostype Ubuntu_64 --registe
```

## To define CPUs and RAM:

```text
$ VBoxManage modifyvm test --cpus 2 --memory 512 --vram 1
```

## To create a bidged NIC:

```text
$ VBoxManage modifyvm test --nic1 bridged --bridgeadapter1 enp3s0f
```

## To allocate a disk:

```text
$ VBoxManage createhd --filename /home/nali/VMVidi/test.vdi --size 1024
```

## To create SATA controller:

```text
$ VBoxManage storagectl test --name "SATA Controller" --add sata --bootable on \
   --port 0 --device 0 --type hdd --medium /home/nali/VMVidi/test.vdi
```

## To attach SATA controller:

```text
$ VBoxManage storageattach test --storagectl "SATA Controller
```

## To load ISO at boot:

```text
$ VBoxManage storageattach test --storagectl "IDE Controller" --port 0  --device 0 --type dvddrive --medium /home/nali/ISO/mini.iso
```

## To detach ISO:

```text
$ VBoxManage storageattach test --storagectl "IDE Controller" --port 0  --device 0 --type dvddrive --medium none
```

## To modify VRDE settings:

```text
$ VBoxManage modifyvm test --vrde on
$ VBoxManage modifyvm test --vrdeaddress 127.0.0.1
```

## To start vm:

```text
$VBoxManage startvm test --type headless
```

## To soft power off:

```text
$ VBoxManage controlvm test acpipowerbutton
```

## To hard power off:

```text
$ VBoxManage controlvm test poweroff soft
```



