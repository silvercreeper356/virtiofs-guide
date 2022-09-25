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

Step 2: Guest
