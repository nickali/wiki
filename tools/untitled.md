# Set up Headless Virtualbox VM
             
### To install Virtualbox
```
$ sudo apt install virtualbox
```

### To install Virtualbox Extension Pack:
```
$ sudo apt install virtualbox-ext-pack
```

### To get list of OSs VirtualBox supports:
```
$ VBoxManage list ostype
```

### To instantiate new VM:
```
$ VBoxManage createvm --name test --ostype Ubuntu_64 --registe
```

### To define CPUs and RAM:
```
$ VBoxManage modifyvm test --cpus 2 --memory 512 --vram 1
```
### To create a bidged NIC:
```
$ VBoxManage modifyvm test --nic1 bridged --bridgeadapter1 enp3s0f
```

### To allocate a disk:
```
$ VBoxManage createhd --filename /home/nali/VMVidi/test.vdi --size 1024
```

### To create SATA controller:
```
$ VBoxManage storagectl test --name "SATA Controller" --add sata --bootable on \
   --port 0 --device 0 --type hdd --medium /home/nali/VMVidi/test.vdi
```

### To attach SATA controller:
```
$ VBoxManage storageattach test --storagectl "SATA Controller
```

### To load ISO at boot:
```
$ VBoxManage storageattach test --storagectl "IDE Controller" --port 0  --device 0 --type dvddrive --medium /home/nali/ISO/mini.iso
```

### To detach ISO:
```
$ VBoxManage storageattach test --storagectl "IDE Controller" --port 0  --device 0 --type dvddrive --medium none
```


### To modify VRDE settings:
```
$ VBoxManage modifyvm test --vrde on
$ VBoxManage modifyvm test --vrdeaddress 127.0.0.1
```

### To start vm:
```
$VBoxManage startvm test --type headles

```
### To power off:

```
$ VBoxManage controlvm test poweroff soft
```


