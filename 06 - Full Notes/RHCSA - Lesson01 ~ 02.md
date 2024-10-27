---
⭕첫 학습날: 2024-07-16
⭕과목: RHCSA
⭕교재: Red Hat Certified System Administrator (RHCSA) 3/e
⭕페이지: Lesson01
⭕학습정도: 🤔중
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: false
복습: 추가 복습
🛑첫날: "✏첫날 : 2024/07/16"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤103일째❤
🛑4일후: "🥉4일뒤 : 2024/07/20"
🛑7일후: "🥈7일뒤 : 2024/07/23"
🛑14일후: "🥇14일뒤 : 2024/07/30"
4일후: "@2024년 7월 20일"
4일후(text): 2024/07/20
7일후: "@2024년 7월 23일"
7일후(text): 2024/07/23
14일후: "@2024년 7월 30일"
14일후(text): 2024/07/30
오늘1: "@2024년 10월 27일 오후 2:02"
오늘2: 2024/10/27
첫학습날text: 2024/07/16
오늘과 첫학습날 사이: "103"
사이: "103"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "0"
학습률: "0.6"
진행바: 🟩🟩🟩🟩🟩🟩⬜⬜⬜⬜ 60%
---
[[Linux]] [[RHCSA]]
### 단서 질문

- 커스텀 파티셔닝이란?
    
    저장장치의 공간의 디렉터리를 설정하는 것.
    
- 마운트란?
    
    리눅스에서 저장 장치를 사용하기 위해서 파일 트리에 파일을 넣는 것을 말한다.
    
- 리다이렉션이란?
    
    리눅스에서 명령어를 실행할 때, 실행하는 명령은 표준 입력이라 하고 명령어로 나오는 결과를 표준 출력, 명령어의 에러가 발생했을 때는 표준 에러라고 말한다.
    
    이러한 표준 에러를 리다이렉션을 통해서 /dev/null로 보내거나 파일에 저장할 수 있다.
    
    ```Bash
    # 표준 에러를 /dev/null로 보낸다.
    find / -name *.conf 2> /dev/null # 에러 메시지가 사라진 결과가 출력된다.
    ```
    
- man이란?
    
    man은 명령어에 대한 사용 설명서를 보여주는 명령어다. man -k [찾는 명령어]를 통해서 명령어를 검색할 수도 있다. 만약, mandb가 업데이트 되지 않았거나 존재하지 않는다면 이를 찾을 수 없으므로 mandb 명령어로 업데이트를 진행한다.
    
    ```Bash
    # 유저 추가 명령어를 찾고 싶은데 뭐더라?
    man -k user | grep ^user
    user_caps (5)        - user-defined terminfo capability format
    useradd (8)          - create a new user or update default new user information
    userdel (8)          - delete a user account and related files
    usermod (8)          - modify a user account
    users (1)            - print the user names of users currently logged in to the current host
    ```
    

### 핵심 필기

- 전체 내용 접기
    
    # 1.3 Installing with Custom Partitioning
    
    여기 실습에선 Standard Partitioning을 사용한다. LVM이 있는데 LVM의 경우 모든 저장 장치를 하나의 LV(Logical Volume, 논리적 저장 장치)로 모은 후에 이를 나눈다.(파티셔닝한다)
    
    물리 저장 장치마다 데이터를 저장하는 방식과 달리 논리적으로 나눠서 효율적으로 관리가 가능하다.
    
    # 2.1 Getting Started with Linux commands
    
    ```Bash
    ls
    whoami
    su - [유저명]
    pwd
    ip addr show
    
    
    # 메모리 사용량을 MB로 출력
    john@john:~$ free -m
                   total        used        free      shared  buff/cache   available
    Mem:           15793        3082         780         887       11930       11442
    Swap:           2048           0        2047
    
    # df(Disk Free) 디스크 사용량을 출력
    john@john:~$ df
    Filesystem     1K-blocks     Used Available Use% Mounted on
    tmpfs            1617272     2420   1614852   1% /run
    /dev/nvme0n1p2 244506940 79177172 152836712  35% /
    tmpfs            8086340   153756   7932584   2% /dev/shm
    tmpfs               5120        4      5116   1% /run/lock
    efivarfs             128       35        89  28% /sys/firmware/efi/efivars
    /dev/nvme0n1p1    520192     6232    513960   2% /boot/efi
    tmpfs            1617268      148   1617120   1% /run/user/1000
    
    john@john:~$ df -m
    Filesystem     1M-blocks  Used Available Use% Mounted on
    tmpfs               1580     3      1578   1% /run
    /dev/nvme0n1p2    238777 77322    149255  35% /
    tmpfs               7897   151      7747   2% /dev/shm
    tmpfs                  5     1         5   1% /run/lock
    efivarfs               1     1         1  28% /sys/firmware/efi/efivars
    /dev/nvme0n1p1       508     7       502   2% /boot/efi
    tmpfs               1580     1      1580   1% /run/user/1000
    
    john@john:~$ df -h # human
    Filesystem      Size  Used Avail Use% Mounted on
    tmpfs           1.6G  2.4M  1.6G   1% /run
    /dev/nvme0n1p2  234G   76G  146G  35% /
    tmpfs           7.8G  102M  7.7G   2% /dev/shm
    tmpfs           5.0M  4.0K  5.0M   1% /run/lock
    efivarfs        128K   35K   89K  28% /sys/firmware/efi/efivars
    /dev/nvme0n1p1  508M  6.1M  502M   2% /boot/efi
    tmpfs           1.6G  148K  1.6G   1% /run/user/1000
    
    # 텍스트를 출력한다.
    john@john:~$ cat /etc/hosts
    127.0.0.1	localhost
    127.0.1.1	john-950XCJ-951XCJ-950XCR
    
    # The following lines are desirable for IPv6 capable hosts
    ::1     ip6-localhost ip6-loopback
    fe00::0 ip6-localnet
    ff00::0 ip6-mcastprefix
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters
    
    # find mount: 시스템에 마운트된 파일시스템을 보여준다.
    john@john:~$ findmnt
    TARGET                                        SOURCE           FSTYPE OPTIONS
    /                                             /dev/nvme0n1p2   ext4   rw,relati
    ├─/sys                                        sysfs            sysfs  rw,nosuid
    │ ├─/sys/kernel/security                      securityfs       securi rw,nosuid
    │ ├─/sys/fs/cgroup                            cgroup2          cgroup rw,nosuid
    │ ├─/sys/fs/pstore                            pstore           pstore rw,nosuid
    │ ├─/sys/firmware/efi/efivars                 efivarfs         efivar rw,nosuid
    │ ├─/sys/fs/bpf                               bpf              bpf    rw,nosuid
    │ ├─/sys/kernel/debug                         debugfs          debugf rw,nosuid
    │ ├─/sys/kernel/tracing                       tracefs          tracef rw,nosuid
    │ ├─/sys/fs/fuse/connections                  fusectl          fusect rw,nosuid
    │ └─/sys/kernel/config                        configfs         config rw,nosuid
    ├─/proc                                       proc             proc   rw,nosuid
    │ └─/proc/sys/fs/binfmt_misc                  systemd-1        autofs rw,relati
    │   └─/proc/sys/fs/binfmt_misc                binfmt_misc      binfmt rw,nosuid
    ├─/dev                                        udev             devtmp rw,nosuid
    │ ├─/dev/pts                                  devpts           devpts rw,nosuid
    │ ├─/dev/shm                                  tmpfs            tmpfs  rw,nosuid
    │ ├─/dev/hugepages                            hugetlbfs        hugetl rw,relati
    │ └─/dev/mqueue                               mqueue           mqueue rw,nosuid
    ├─/run                                        tmpfs            tmpfs  rw,nosuid
    │ ├─/run/lock                                 tmpfs            tmpfs  rw,nosuid
    │ ├─/run/credentials/systemd-sysusers.service ramfs            ramfs  ro,nosuid
    │ ├─/run/snapd/ns                             tmpfs[/snapd/ns] tmpfs  rw,nosuid
    │ │ ├─/run/snapd/ns/canonical-livepatch.mnt   nsfs[mnt:[4026532658]]
    │ │ │                                                          nsfs   rw
    │ │ ├─/run/snapd/ns/snapd-desktop-integration.mnt
    │ │ │                                         nsfs[mnt:[4026532672]]
    │ │ │                                                          nsfs   rw
    │ │ └─/run/snapd/ns/snap-store.mnt            nsfs[mnt:[4026532827]]
    │ │                                                            nsfs   rw
    │ ├─/run/user/1000                            tmpfs            tmpfs  rw,nosuid
    │ │ ├─/run/user/1000/doc                      portal           fuse.p rw,nosuid
    │ │ └─/run/user/1000/gvfs                     gvfsd-fuse       fuse.g rw,nosuid
    │ └─/run/docker/netns/07ec35c60998            nsfs[net:[4026532839]]
    │                                                              nsfs   rw
    ├─/snap/bare/5                                /dev/loop0       squash ro,nodev,
    ├─/snap/canonical-livepatch/278               /dev/loop1       squash ro,nodev,
    ├─/snap/canonical-livepatch/282               /dev/loop2       squash ro,nodev,
    ├─/snap/core18/2823                           /dev/loop3       squash ro,nodev,
    ├─/snap/core18/2829                           /dev/loop4       squash ro,nodev,
    ├─/snap/core20/2264                           /dev/loop5       squash ro,nodev,
    ├─/snap/core20/2318                           /dev/loop6       squash ro,nodev,
    ├─/snap/core22/1122                           /dev/loop7       squash ro,nodev,
    ├─/snap/core22/1380                           /dev/loop8       squash ro,nodev,
    ├─/snap/firefox/4483                          /dev/loop9       squash ro,nodev,
    ├─/snap/firefox/4539                          /dev/loop10      squash ro,nodev,
    ├─/snap/gnome-3-34-1804/93                    /dev/loop11      squash ro,nodev,
    ├─/snap/gnome-3-38-2004/143                   /dev/loop12      squash ro,nodev,
    ├─/snap/gnome-42-2204/120                     /dev/loop13      squash ro,nodev,
    ├─/snap/gnome-42-2204/176                     /dev/loop14      squash ro,nodev,
    ├─/snap/gtk-common-themes/1535                /dev/loop15      squash ro,nodev,
    ├─/snap/shortwave/87                          /dev/loop16      squash ro,nodev,
    ├─/snap/shortwave/89                          /dev/loop17      squash ro,nodev,
    ├─/snap/slack/149                             /dev/loop18      squash ro,nodev,
    ├─/snap/slack/153                             /dev/loop19      squash ro,nodev,
    ├─/snap/snap-store/1113                       /dev/loop20      squash ro,nodev,
    ├─/snap/snap-store/959                        /dev/loop21      squash ro,nodev,
    ├─/snap/snapd/21465                           /dev/loop22      squash ro,nodev,
    ├─/snap/snapd/21759                           /dev/loop23      squash ro,nodev,
    ├─/snap/snapd-desktop-integration/157         /dev/loop24      squash ro,nodev,
    ├─/snap/snapd-desktop-integration/83          /dev/loop25      squash ro,nodev,
    ├─/var/snap/firefox/common/host-hunspell      /dev/nvme0n1p2[/usr/share/hunspell]
    │                                                              ext4   ro,noexec
    ├─/snap/vlc/3777                              /dev/loop26      squash ro,nodev,
    ├─/boot/efi                                   /dev/nvme0n1p1   vfat   rw,relati
    └─/var/lib/docker/overlay2/705f20cc48207cdb4e308820e227781c8dc1a11322aab74ceacc991c9e38b748/merged
                                                  overlay          overla rw,relati
    ```
    
    # 2.2 Working with the Bash Shell
    
    ```Bash
    history
    ![[명령할 숫자]
    ```
    
    - 실제 실행 예시
        
        ```Bash
        john@john:~$ history
            1  sudo apt autoremove 
            2  sudo apt update
            3  sudo apt upgrade
            4  clear
            5  bleachbit
            6  sudo apt install bleachbit 
            7  clear
            8  bleachbit 
            9  sudo bleachbit 
           10  pulseaudio --help
           11  pulseaudio 
           12  pulseaudio --kill
           13  pulseaudio 
           14  sudo pulseaudio --kill
           15  systemctl --user restart pipewire.service 
           16  systemctl --user restart pipewire-media-session.service 
           17  find /etc/ -name Ubuntu
           18  sudo find /etc/ -name Ubuntu*
           19  sudo find /etc/ -name ubuntu*
           20  lsb_release -a
           21  pulseaudio --kill
           22  pulseaudio --start
           23  pulseaudio -k
           24  reboot
           25  sudo apt remove imagemagick
           26  sudo apt remove imagemagick*
           27  clear
           28  sudo apt remove -y firefox
           29  plank
           30  plank --preferences
           31  cat /etc/init/cron.conf
           32  sudo cat /etc/init/cron.conf
           33  ㅔㄴ
           34  ps
           35  ps aux
           36  ps aux | grep plank
           37  sudo systemctl enable plank.service
           38  find -name ".config"
           39  ls
           40  ls -al
           41  ls -al | grep ".config"
           42  cd .config/
           43  ls
           44  cd autostart/
           45  ls
           46  ls m-al
           47  ls -al
           48  touch plank.desktop
           49  ls
           50  sudo chmod 770 plank.desktop 
           51  ls
           52  ls -al
           53  vim plank.desktop 
           54  clear
           55  sudo virtualbox
           56  virtualbox
           57  su - root
           58  hostnamectl 
           59  hostnamectl --help
           60  free -m
           61  df
           62  clear
           63  df
           64  df -m
           65  clear
           66  df
           67  df -m
           68  clear
           69  df -h
           70  clear
           71  df -h
           72  grep --help | re*
           73  grep --help | grep re*
           74  grep --help | grep rege*
           75  clear
           76  cat /etc/hosts
           77  findmnt
           78  clear
           79  history
        john@john:~$ !60
        free -m
                       total        used        free      shared  buff/cache   available
        Mem:           15793        3942        1696         756       10154       10761
        Swap:           2048           0        2047
        ```
        
    - reverse-i-search
        
        이전 실행한 명령어를 검색할 수 있음. 셀에서 ctrl + R 버튼으로 사용 가능하다.
        
    - piping
        
        이전 명령어 실행의 결과물일 입력으로 사용 가능하다.
        
        ```Bash
        ps aux | less
        ps aux | wc
        ```
        
    - redirection
        
        |**리다이렉션 기호**|**방향**|**의미**|
        |---|---|---|
        |>|표준 출력|명령 > 파일: 명령의 결과를 파일로 저장|
        |>>|표준 출력(이어쓰기)||
        |<|표준 입력|명령 < 파일: 파일의 데이터를 명령에 입력|
        
        실행 결과나 에러 메시지를 다른 곳으로 보낼 수 있다.
        
        [https://inpa.tistory.com/entry/리눅스-devnull-리다이렉션-기호-종류#파일_디스크립터](https://inpa.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-devnull-%EB%A6%AC%EB%8B%A4%EC%9D%B4%EB%A0%89%EC%85%98-%EA%B8%B0%ED%98%B8-%EC%A2%85%EB%A5%98#%ED%8C%8C%EC%9D%BC_%EB%94%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%84%B0)
        
        ```Bash
        john@john:~$ ls | head -1 > lsfiles
        john@john:~$ cat lsfiles 
        다운로드
        john@john:~$ ls | head -2 >> lsfiles 
        john@john:~$ cat lsfiles 
        다운로드
        다운로드
        2024-06-28-13-58-17.092-VBoxSVC-4571.log
        ```
        
    - environment variables
        
        env를 통해서 bash 셸에서 사용되는 환경변수를 볼 수 있다.
        
    
    # 2.3 Understaing I/O Redirection and Piping
    
    >: standard output를 출력
    
    >>: standard output 덧붙이기
    
    2>: standard error를 출력
    
    <:
    
    ```Bash
    # Permission denied는 에러 메시지이므로
    # 표준 에러메시지가 리다이렉션된 /dev/null로 넘어간다.
    find / -type f -name *.conf 2> /dev/null
    ```
    
    # 2.4 Understanding the Linux File System Hierarchy
    
    리눅스의 파일시스템은 FHS(File Hierachy System) 표준을 따른다. 이는 리눅스 단체에서 정한 표준이다.
    
    /boot: 부팅에 사용되는 명령어들이 있다.
    
    /dev: 디바이스들을 다루는 곳이다.
    
    /home: 사용자 디렉터리로 유저별로 디렉터리가 존재한다.
    
    /home/[유저명]
    
    /etc: 설정값들이 저장된 곳이다.
    
    /var: 가변적인 값들이 저장되는 곳이다. 로그가 여기 저장된다.
    
    /usr: 리눅스에 핵심 명령어 및 사용자 명령어가 있다.
    
    /usr/bin: 실행 가능한 이진코드들이 있다.
    
    /usr/sbin: 시스템 바이너리로 시스템을 위한 이진코드들이 있다.
    
    > [!important]  
    > 마운트란? 저장 장치를 사용하기 위해서 리눅스 파일 시스템 트리에 부착하는 것.  
    
      
    
    # 2.6 Using Man
    
    …: 여러 개 입력 가능
    
    man을 사용하는 흐름도
    
    ```Bash
    # 검색하고 싶은 man이 있는데 옵션을 뭐 써야할지 잘 모르겠다.
    # -> man man
    man man
    -k: aprpos 어쩌구
    # /로 apropos를 찾는다.
    apropos is ...
    
    # apropos는 명령어이므로 bold 처리되어 있다. 
    # 이제 aprpos를 검색한다
    man apropos
    mandb is ..
    # manddb를 찾았다 mandb를 검색한다.
    man mandb
    MANDB(8)                                                            Manual pager utils                                                            MANDB(8)
    
    NAME
           mandb - create or update the manual page index caches
    
    SYNOPSIS
    # mandb가 man 정보를 업데이트하거나 만들 수 있다는 것을 알 수 있다.
    manddb
    # 이제 원하는 명령어를 찾는다.
    man -k user
    ```
    
    # 2.7 Using Vim
    
    ```Bash
    gg: 맨앞문서로
    G: 문서 맨 뒤로
    
    u: undo 취소
    Ctrl+r: 되돌리기
    ^: 라인 시작
    $: 라인 끝
    ```
    
    # 2.8 Globbing
    
    파일 이름 매칭해주는 기능. 정규식이랑 다름
    
    ```Bash
    ls ?abc
    dabc
    aabc
    cabc
    
    ls [ab]cd
    acd
    bcd
    
    ls [!ab]cd
    ccd
    dcd
    ecd
    ```
    

### 핵심 요약

- 핵심 요약 접기

### 복습알림

> [!important]  
>   


  