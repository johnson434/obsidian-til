---
기술:
  - Linux
  - OS
---
[[Linux]]
# /dev

연결된 장치를 나타내는 파일을 포함한 특수 디렉터리를 가지고 있다.

## sda

sd 뒤에 오는 알파벳을 메이저 넘버(major number)라고 한다.  
sda = 첫번째 하드드라이브  
sdb = 두번째 하드드라이브  
sdc = 세번째 하드드라이브  
sdd = 네번째 하드드라이브  
드라이브는 파티션으로 나눌 수 있음.  
sda - sda1 + sda2 + sda3 .. sdn(sd 뒤에 오는 숫자를 마이너 넘버(minor number)라고 한다)  

## 문자(character) 장치

c(character)로 시작하는 파일이나 디렉터리는 문자 단위로 데이터를 송수신하여 시스템과 상호작용하는 문자 장치를 뜻한다.

키보드도 문자 장치에 속한다.

```Shell
ls -al /dev | grep ^c | head -n 10
```

## 블록(block) 장치

b(block)로 시작하면 블록 장치를 뜻한다. 데이터를 블록(한 번에 여러 바이트)으로 통신한다.

```Shell
ls -al /dev | grep ^b | tail -n 4
brw-rw----   1 root  disk      259,     1  3월  6 12:41 nvme0n1p1
brw-rw----   1 root  disk      259,     2  3월  6 12:41 nvme0n1p2
brw-rw----   1 root  disk      259,     3  3월  6 12:41 nvme0n1p3
brw-rw----   1 root  disk      259,     4  3월  6 12:41 nvme0n1p4
```

  

**lsblk(list block)** : 블록 장치 및 정보 나열

```Shell
hwang@hwang:~$ lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0         7:0    0 946.1M  1 loop /snap/clion/263
loop1         7:1    0     4K  1 loop /snap/bare/5
loop2         7:2    0 946.2M  1 loop /snap/clion/265
loop3         7:3    0  55.7M  1 loop /snap/core18/2796
loop4         7:4    0  55.7M  1 loop /snap/core18/2812
loop5         7:5    0  63.9M  1 loop /snap/core20/2105
loop6         7:6    0  63.9M  1 loop /snap/core20/2182
loop7         7:7    0  74.1M  1 loop /snap/core22/1033
loop8         7:8    0  74.2M  1 loop /snap/core22/1122
loop9         7:9    0   6.4M  1 loop /snap/curl/1754
loop10        7:10   0 262.5M  1 loop /snap/firefox/3779
loop11        7:11   0 266.6M  1 loop /snap/firefox/3836
loop12        7:12   0 349.7M  1 loop /snap/gnome-3-38-2004/143
loop13        7:13   0 485.5M  1 loop /snap/gnome-42-2204/120
loop14        7:14   0  12.3M  1 loop /snap/snap-store/959
loop15        7:15   0   497M  1 loop /snap/gnome-42-2204/141
loop16        7:16   0  91.7M  1 loop /snap/gtk-common-themes/1535
loop17        7:17   0  40.9M  1 loop /snap/snapd/20290
loop18        7:18   0  40.4M  1 loop /snap/snapd/20671
loop19        7:19   0   452K  1 loop /snap/snapd-desktop-integration/83
nvme0n1     259:0    0 238.5G  0 disk 
├─nvme0n1p1 259:1    0   512M  0 part /boot/grub
│                                     /boot/efi
├─nvme0n1p2 259:2    0     2G  0 part [SWAP]
├─nvme0n1p3 259:3    0     2G  0 part 
└─nvme0n1p4 259:4    0   234G  0 part 
```

## 마운트

마운트는 저장 장치를 논리적으로 연결하는 행위다.

대부분의 운영체제는 물리적으로 연결하면 자동적으로 논리적으로 연결된다.

이를 직접하려면 마운트/언마운트를 사용한다.

```Shell
mount /dev/sdb1
umount /dev/sdb1
```

  

/root : 전지전능한 루트 사용자의 홈 디렉터리

/etc : 리눅스 환경 설정 파일을 포함한다. 프로그램 시작을 언제 어떻게 할 것인지 제어하는 파일.

/home : 사용자의 홈 디렉터리다.

/mnt : 다른 파일 시스템이 파일 시스템에 연결되거나 마운트되는 위치.

/media : 보통 CD나 USB 장치가 파일 시스템에 연결되거나 마운트되는 위치이다.

/bin : 애플리케이션 바이너리(실행 파일)가 위치하는 곳이다.

/lib : 라이브러리가 위치한다.