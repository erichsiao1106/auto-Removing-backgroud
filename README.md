# 安裝系統

- JetPack下載：[https://developer.nvidia.com/embedded/jetpack](https://developer.nvidia.com/embedded/jetpack)
    - JetPack 4.4 內相關套件版本
        - TensorRT 7.1.3
        - cuDNN 8.0
        - CUDA 10.2
        - OpenCV 4.1.1
- 燒錄image檔案到SD卡（或從SD備份映像檔燒錄）
    - 使用balenaEtcher: [https://www.balena.io/etcher/](https://www.balena.io/etcher/)
    - 使用rufus: [https://rufus.ie/](https://rufus.ie/)
    - 已把jetson nano從SD備份(使用rufus)的映像檔(30GB)壓縮成zip檔(7GB) [ 要用7-Zip解壓縮軟體解壓縮，否則無法燒錄到SD卡裡 ]: [https://drive.google.com/drive/folders/1dSqKI6-TU0pfpJU3UAW7j0_wMPmCWj-9](https://drive.google.com/drive/folders/1dSqKI6-TU0pfpJU3UAW7j0_wMPmCWj-9)
- [補充] [Backup Raspberry Pi SD Card on macOS](https://medium.com/@ccarnino/backup-raspberry-pi-sd-card-on-macos-the-2019-simple-way-to-clone-1517af972ca5)
- 映像檔開機
- 連接網路

## 遠端連線

- Get current IP address: $`ifconfig`

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57b03d08-a6eb-4f98-923e-6d52dbcb9c7f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57b03d08-a6eb-4f98-923e-6d52dbcb9c7f/Untitled.png)

- 以SSH連線 (以上圖為例)
    - ssh ai-nano@192.168.0.112 (ip位址由ifconfig查詢)
- 傳輸檔案：使用SFTP連線（可用Filezilla或Terminal）
    - sftp ai-nano@192.168.0.112 (ip位址由ifconfig查詢)

## 設定SWAP為8G

- 查看SWAP狀態 $ `free -h`

```bash
sudo fallocate -l 8G /swapfile
sudo chmod 600 /swapfile
ls -lh /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo swapon -show
sudo bash -c 'echo "/var/swapfile swap swap defaults 0 0" >> /etc/fstab'
```

## 移除 libreoffice

```bash
sudo apt-get purge libreoffice*
sudo apt-get clean
```

## 安裝pip —> [REF](https://blog.csdn.net/beckhans/article/details/89146881)

- 先更新apt-get $ `sudo apt-get update`
- ~~$`sudo apt-get install python3-pip`~~
- $`sudo apt-get install python3-pip python3-dev`
- $`python3 -m pip install --upgrade pip`
- $`sudo vim /usr/bin/pip3`

    ```python
    # REPLACE
    # from pip import mai
    # if __name__ == '__main__':
        # sys.exit(main())

    # BY
    from pip import __main__
    if __name__ == '__main__':
        sys.exit(__main__._main())
    ```

    — 
