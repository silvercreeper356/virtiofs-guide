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


