# 마나토끼, 뉴토끼 만화 다운로더 + 뷰어 + Webdav

나스, 리눅스 서버 용 백그라운드 다운로더 feat. `docker` (_manatoki_, *newtoki*만 가능)

이 프로그램은 아래 기능을 포함하고 있습니다

- manatoki 만화 다운로더
  - 다운로드가 완료되면 zip으로 저장
  - 주기적인 스캔기능 (신규 업로드가 있으면 자동 다운로드)
  - 설정에 의한 동시 다운로드
- [komga](https://komga.org/) (만화책 뷰어)
- [webdav](https://hub.docker.com/r/ugeek/webdav) (mobile app 용)

manatoki downloader + [webdav](https://hub.docker.com/r/ugeek/webdav) + [komga](https://komga.org/)

# 완료 메세지

다운로드가 완료되고, 압축이 완료가 되면 `complete-noti.sh`가 실행이 됩니다.

해당 스크립트의 기본 목적은 새로운 만화 다운로드가 완료되었을 때 telegram으로 noti를 보내기 위함입니다.  
*BOT_TOKEN과 CHAT_ID*를 추가하고 주석 풀어 사용하면 됩니다

[BOT_TOKEN과 CHAT_ID 얻기 참고](https://gabrielkim.tistory.com/entry/Telegram-Bot-Token-%EB%B0%8F-Chat-Id-%EC%96%BB%EA%B8%B0)

압축이 완료된 후 무언가 다른 작업을 하고 싶으면 스크립트를 바꾸시면 됩니다.

스크립트의 첫번째 param은 `완료 메세지`  
두번째 param은 `zip 파일 경로`입니다. 혹시 unzip이 필요할 수도 있기에...

# 사용법

1. `docker-compose.yml`파일을 열어서 `dist-youngs-downloder`의 _PUID_, _PGID_ `dist-webdav`의 _UID_, _GID_, `dist-komga`의 _user_ 항목을 수정
   1. 리눅스의 현재 로그인 한 계정의 UID/GID와 같은 것으로 셋팅해야함
1. `webdav`와 `komga`의 원하는 포트번호로 수정
1. `webdav`의 *username/password*부분을 원하는 사용자/패스워드로 수정
1. `wishlist.json`에 원하는 만화 목록을 추가한다
   1. `title`은 아무거나 가능
   1. `url`은 반드시 그 만화의 전체 리스트가 나오는 url이어야함
1. 마지막으로 아래 명령 실행

```sh
docker-compose up -d --build
```

# Tips

1. 동작중에 `wishlist.json`를 업데이트하면, *docker-compose restart*로 컨테이너를 재시작해야함
1. `wishlist.json`의 *period*는 스캔 시간을 의미함. `300`보다 작을 수 없음 (단위 초)
1. `wishlist.json`의 *threads*는 동시에 몇개를 다운로드 할지 정하는 값. `0`이 되면 절대 안됨
1. domain이 변경되는 경우가 간혹 있어서, 로그는 가끔 체크해주셔야합니다. 로그에 보면 주소를 못찾아서 error가 쭉 뜨는게 보입니다.

# 주의사항

- `만화`와 `웹툰` 둘다 다운로드가 가능하긴 한데.. `웹툰`은 테스트를 많이 안해봤음
- 해당 프로그램을 이용하여 발생하는 모든 상황에 대해, 제작자는 어떠한 책임도 지지 않습니다
- 해당 프로그램으로 제작자는 어떠한 금전적 이득을 취하지 않습니다

# How to use

1. Open `docker-compose.yml` and set proper _PUID_, _PGID_ for `dist-youngs-downloder` and _UID_, _GID_ for `dist-webdav` and _user_ for `dist-komga`
   1. You have to set UID/GID you are currently logged in on the host
1. Set proper `port number` for `webdav` and `komga`.
1. Set `webdav` _username/password_
1. Add items to `wishlist.json`.
   1. `title` can be any string.
   1. `url` **MUST** be the url of list of series
1. Finally run below:

# Tips

1. If you update `wishlist.json` while running, you must restart docker container with `docker-compose restart` to apply
1. _period_ in `wishlist.json` means scan period. It can't be less than `300` seconds
1. _threads_ in `wishlist.json` means how many comics can be downloaded simultaneously. MUST NOT BE `0`

```sh
docker-compose up -d --build
```
