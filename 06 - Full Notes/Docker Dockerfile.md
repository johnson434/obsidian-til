---
기술:
  - Docker
---
[[Docker]] [[Dockerfile]]
> [!info] Dockerfile reference  
> Find all the available commands you can use in a Dockerfile and learn how to use them, including COPY, ARG, ENTRYPOINT, and more.  
> [https://docs.docker.com/reference/dockerfile/](https://docs.docker.com/reference/dockerfile/)  

|   |   |
|---|---|
|**Instruction**|**Description**|
|[`ADD`](https://docs.docker.com/reference/dockerfile/#add)|Add local or remote files and directories.|
|[`ARG`](https://docs.docker.com/reference/dockerfile/#arg)|Use build-time variables.|
|[`CMD`](https://docs.docker.com/reference/dockerfile/#cmd)|Specify default commands.|
|[`COPY`](https://docs.docker.com/reference/dockerfile/#copy)|Copy files and directories.|
|[`ENTRYPOINT`](https://docs.docker.com/reference/dockerfile/#entrypoint)|Specify default executable.|
|[`ENV`](https://docs.docker.com/reference/dockerfile/#env)|Set environment variables.|
|[`EXPOSE`](https://docs.docker.com/reference/dockerfile/#expose)|Describe which ports your application is listening on.  <br>Container가 Listening할 Port 번호|
|[`FROM`](https://docs.docker.com/reference/dockerfile/#from)|Create a new build stage from a base image.|
|[`HEALTHCHECK`](https://docs.docker.com/reference/dockerfile/#healthcheck)|Check a container's health on startup.|
|[`LABEL`](https://docs.docker.com/reference/dockerfile/#label)|Add metadata to an image.|
|[`MAINTAINER`](https://docs.docker.com/reference/dockerfile/#maintainer-deprecated)|Specify the author of an image.|
|[`ONBUILD`](https://docs.docker.com/reference/dockerfile/#onbuild)|Specify instructions for when the image is used in a build.|
|[`RUN`](https://docs.docker.com/reference/dockerfile/#run)|Execute build commands.|
|[`SHELL`](https://docs.docker.com/reference/dockerfile/#shell)|Set the default shell of an image.|
|[`STOPSIGNAL`](https://docs.docker.com/reference/dockerfile/#stopsignal)|Specify the system call signal for exiting a container.|
|[`USER`](https://docs.docker.com/reference/dockerfile/#user)|Set user and group ID.|
|[`VOLUME`](https://docs.docker.com/reference/dockerfile/#volume)|Create volume mounts.|
|[`WORKDIR`](https://docs.docker.com/reference/dockerfile/#workdir)|Change working directory.|

![[Untitled 10.png]]

# ADD vs COPY

ADD

- src가 압축 파일이면 자동으로 압축 해제 후에 복사

COPY

- host 환경의 파일 또는 디렉터리를 복사한다.