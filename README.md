# virtiofs-guide
Guide for using virtiofs to share a filesystem from a Linux host to a Windows guest.

Video Guide: [WIP]

This guide goes through setting up virtiofs to share files to a Windows guest. Also possible with Linux guests but this guide only covers Windows.

Step 1: Configure in Virtual Machine Manager

Enable Shared Memory and Apply

![ShareX_a2HPjjj7Jt](https://user-images.githubusercontent.com/76752846/192163739-b2e59ff2-03d0-4346-8d01-9d5180ce957f.png)

Go to Add Hardware > Filesystem
Open XML tab and paste in this (You might have to enable XML Editing)

        <filesystem type='mount' accessmode='passthrough'>
          <driver type='virtiofs' queue='1024'/>
          <source dir='/Path-to-Source'/>
          <target dir='share-name-in-guest'/>
        </filesystem>
      
Press Finish 

![2022-09-25_17-59](https://user-images.githubusercontent.com/76752846/192167448-6b037e37-4739-4c3f-a6d6-0c39c637c4a7.png)

Step 2: Install required guest software

Download and install virtio guest tools

latest download: https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/latest-virtio/virtio-win-guest-tools.exe

![chrome_lGqrtRAdqg](https://user-images.githubusercontent.com/76752846/192167723-cd52cbd5-4c1b-485c-b020-aebc86a77079.png)

You may need to reboot

Download and install WinFsp

latest download: https://github.com/billziss-gh/winfsp/releases/latest

![msiexec_OeWhd25rQx](https://user-images.githubusercontent.com/76752846/192167786-b55f3760-0dc5-481d-9d2d-1ef8676474c2.png)

Step 3: Install virtio storage drivers

!!!!ONLY IF You dont have virtio storage drivers already installed!!!!

Download latest virtio-win ISO: https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso

Mount ISO in Windows:

![chrome_ztyax7jRKS](https://user-images.githubusercontent.com/76752846/192167916-148cb231-2c81-4982-a925-c6738957210f.png)

Open Device Manager > Other Devices > Right click 'Mass Storage Controller' > Update Driver

![chrome_8diRh5b8yN](https://user-images.githubusercontent.com/76752846/192167960-56dd218c-8642-4ea2-afba-3aa00cbee4e5.png)

Click 'Browse my computer for drivers' then 'Browse'

Pick your mounted ISO and click OK

![chrome_VumkFnsjsV](https://user-images.githubusercontent.com/76752846/192167991-209d84ba-d107-4f34-992c-f37a358d4a75.png)

Windows should install drivers, click Close

(You might want to install drivers for any other virtio devices)

Step 4: Manually start Virtio-FS Service

Open 'Run' (Windows Key + R) and run 'Services.msc'

![explorer_0Ylj3FjGGB](https://user-images.githubusercontent.com/76752846/192168057-506b0ff2-468d-4091-a7df-3aee4a43a93f.png)

Scroll down to 'Virtio-FS Service' > Open properties

Set 'Startup type' to Automatic and press 'Start' then 'Apply'

![mmc_oKeCgqNHk0](https://user-images.githubusercontent.com/76752846/192168109-bcd79734-e84e-4d27-b2dc-a37deef37fb8.png)

Reboot

You should be able to open your Host Z: drive in windows

![chrome_kynQ7aJBRH](https://user-images.githubusercontent.com/76752846/192168134-a82191f8-1dde-4914-acbc-39fb1af940e1.png)

If you can't then make sure VirtIO-FS Services is running

Step 5 (Extra): Mounting an existing folder to your shared folder

This is useful for adding other filesystems that aren't already in your shared folder

mkdir NAME
sudo mount -o bind /SOURCE /DEST

UNMOUNT using
sudo umount /DEST
