# Intro

manatoki downloader + [webdav](https://hub.docker.com/r/ugeek/webdav) + [komga](https://komga.org/)

# How to use

1. Open `docker-compose.yml` and set proper `PUID`, `PGID` for `dist-youngs-downloder` and `UID`, `GID` for `dist-webdav` and `user` for dist-komga
   1. You have to set UID/GID you are currently logged in on the host
1. Set proper `port number` for `webdav` and `komga`.
1. Set `webdav` `username/password`
1. Add items to `wishlist.json`.
   1. `title` can be any string.
   1. `url` **MUST** be the url of list of series
1. Finally run below:

# Tips

1. If you update `wishlist.json` while running, you must restart docker container with `docker-compose restart` to apply
1. `period` in `wishlist.json` means scan period. It can't be less than `300`
1. `threads` in `wishlist.json` means how many comics can be downloaded simultaneously. MUST NOT BE `0`

```sh
docker-compose up -d --build
```

# 사용법

1. `docker-compose.yml`파일을 열어서 `dist-youngs-downloder`의 `PUID`, `PGID` `dist-webdav`의 `UID`, `GID` `dist-komga`의`user` 항목을 수정
   1. 리눅스의 현재 로그인 한 계정의 UID/GID와 같은 것으로 셋팅해야함
1. `webdav`와 `komga`의 원하는 포트번호로 수정
1. `webdav`의 `username/password`부분을 원하는 사용자/패스워드로 수정
1. `wishlist.json`에 원하는 만화 목록을 추가한다
   1. `title`은 아무거나 가능
   1. `url`은 반드시 그 만화의 전체 리스트가 나오는 url이어야함
1. 마지막으로 아래 명령 실행

```sh
docker-compose up -d --build
```

# Tips

1. 동작중에 `wishlist.json`를 업데이트하면, `docker-compose restart`로 컨테이너를 재시작해야함
1. `wishlist.json`의 `period`는 스캔 시간을 의미함. `300`보다 작을 수 없음
1. `wishlist.json`의 `threads`는 동시에 몇개를 다운로드 할지 정하는 값. `0`이 되면 절대 안됨
