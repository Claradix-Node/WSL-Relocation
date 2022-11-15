# WSL-Relocation
This repository is for whom is having storage issues and want to change the location of WSL virtual driver which is capturing huge amount of storage.

_The WSL 2 VM disk images would normally reside in:_
```
%USERPROFILE%\AppData\Local\Docker\wsl
```

First, shut down your docker desktop by right click on the Docker Desktop icon and select Quit Docker Desktop
Then, open your command prompt:
```
wsl --list -v
```

You should be able to see, make sure the STATE for both is Stopped.
```
wsl --shutdown
```

```
  NAME                   STATE       VERSION
* docker-desktop        Stopped         2
  docker-desktop-data   Stopped         2
```

Export docker-desktop-data into a file
```
wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"
wsl --export docker-desktop "D:\Docker\wsl\data\docker-desktop.tar"
```

Unregister docker-desktop-data and docker-desktop from wsl, note that after this, your ext4.vhdx file would automatically be removed
```
wsl --unregister docker-desktop-data
wsl --unregister docker-desktop
```

Import the docker-desktop-data back to wsl, but now the ext4.vhdx would reside in different drive/directory:
```
wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2
wsl --import docker-desktop "D:\Docker\wsl\distro" "D:\Docker\wsl\data\docker-desktop.tar" --version 2
```

Start the Docker Desktop again and it should work

You may delete the `D:\Docker\wsl\data\docker-desktop-data.tar` and `D:\Docker\wsl\data\docker-desktop.tar` files.
