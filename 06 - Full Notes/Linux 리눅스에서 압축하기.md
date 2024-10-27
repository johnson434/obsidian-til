---
기술:
  - Linux
---
[[Linux]] [[Linux CLI]]
# tar(tape archive)

```Shell
tar -cvf [지정할 파일] [파일명 파일명 파일명]
# -c(create) : 생성
# -v(verbose) : tar가 다루는 파일을 출력한다.
# -f : 다음에 지정된 파일에 작성하라는 뜻이다.
tar -cvf TarFile.tar file1 file2 file3

# 압축 해제하기
# -x(extract) : 압축해제
# 해제 과정에서 중복되는 파일이 있으면 삭제 후에 대체한다.
tar -xf TarFile.tar
```

# gzip(.tar.gz || .tgz)

```Shell
gzip [파일명]
gunzip [파일명]
```

# bzip2(.tar.bz2)

```Shell
bzip [파일명]
bunzip [파일명]
```

# compress(.tar.Z)

```Shell
compress [파일명]
uncompress [파일명]
```