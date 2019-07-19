---
layout: post
title:  "Learning Shell 2"
date:   2019-07-18 13:45:00 +0900
categories: [Language]
---
* TOC
{:toc}

# 참고서

"**리눅스 커맨드라인 완벽 입문서**"를 읽고 정리하였습니다.

# 리다이렉션

커맨드라인에는 **입출력 방향 지정(I/O 리다이렉션)**이라는 멋진 기능이 있습니다. I/O은 **입력/출력**을 뜻하고, 명령은 리다이렉션을
통해 파일로부터 입력받을 수 있고, 또한 파일로 출력할 수 있습니다. 뿐만 아니라 강력한 명령어 **파이프라인**을 만들기 위해서 필요한 
명령어들을 연결할 수 있습니다.

### 표준 입출력과 표준 오류

""모든 것은 파일이다""라는 유닉스 정신을 상기해보면 ls와 같은 프로그램은 사실 **표준 출력(stdout)**이라고 불리는 특수한 파일에
이 명령어에 대한 결과를 보내고 **표준 오류**라는 또 다른 파일에 그 상태 메세지를 전송합니다. 기본적으로 표준 출력과 오류 모두 화면에 연결되어 있고
디스크 파일에 따로 저장되지 않습니다. 게다가 많은 프로그램들이 **표준입력**이라고 부르는 곳에서 입력 내용을 가져오고 그것은 기본적으로
키보드에 직접 연결되어 있다.

#### cat - 파일 연결하기

**cat 명령어**는 다음과 같이 하나 이상의 파일을 읽어 들여서 표준 출력으로 그 내용을 복사합니다.

> cat [file...]

### 파이프 라인

파이프 연산자인 \| 기호를 사용해서 명령어의 표준 출력을 또 다른 명령어의 표준 입력과 연결시킬 수 있습니다.

> command1 \| command2


#### sort - 텍스트 라인 정렬하기

파이프라인은 데이터의 복잡한 연산을 수행할 때 종종 사용됩니다. 하나의 파이프라인에 여러 명렁어를 입력하는 것이 가능합니다. 주로 이러한 
방식을 사용하는 명령어들을 **필터**라고 합니다. 필터 중 하나로 **sort 명령어**가 있습니다.

```shell

[me@linuxbox ~]$ ls /bin /usr/bin | sort | less

```

파이프라인에 sort를 포함함으로써 하나로 정렬된 데이터 목록으로 바꿀 수 있었습니다.

#### uniq - 중복 줄을 알리거나 생략하기

uniq 명령어는 종종 sort와 연결하여 사용합니다. **uniq 명령어**는 표준 입력이나 하나의 파일명 인자로부터 정렬된 데이터 
목록을 입력받아 중복된 내용을 제거해줍니다. 중복된 내용을 보고 싶다면 -d 옵션을 사용하면 됩니다.

```shell

[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq | less

```

#### wc - 각 파일의 개행 및 단어 개수, 파일 바이트 출력하기

**wc 명령어**는 파일에 들어있는 단어 및 라인의 개수와 파일 크기를 표시해줍니다. 
-l 옵션은 라인 수만 보고 싶을 때 사용할 수 있습니다.

#### grep - 패턴과 일치하는 라인 출력하기

**grep 명령어**는 파일의 텍스트 패턴을 찾을 때 사용하는 강력한 프로그램입니다.

> grep pattern [file...]

grep은 **정규 표현식**이라고 하는 고급 수준의 패턴이나 간단한 패턴으로 파일 내에서 패턴을 만났을 때, 그 패턴을 가지고 있는 라인을 출력합니다.
-I 옵션은 검색을 수행할 때 대소문자를 구분하지 않도록 하고, -v 옵션은 패턴과 일치하지 않는 라인만 출력하도록 합니다.

#### head - 파일의 첫 부분 출력하기

**head 명령어**로 파일의 첫 10줄만 출력할 수 있습니다. -n 옵션을 사용하면 길이를 조절할 수 있습니다.

#### tail - 파일의 마지막 부분 출력하기

**tail 명령어**로 파일의 마지막 10줄을 출력할 수 있습니다. -n 옵션을 사용하면 길이를 조절할 수 있습니다. tail 명령어는 실시간으로 파일을
확인할 수 있는 옵션을 지원합니다. 로그파일이 기록되는 동안 최근 내용을 확인할 때 매우 편리합니다. -f 옵션을 사용하면, tail은 지속적으로 로그
파일을 감시하고 새 내용이 추가될 때 곧바로 그 내용을 표시합니다.

#### tee - 표준 입력을 읽고 표준 출력 및 파일에 쓰기

**tee 프로그램**은 표준 입력으로부터 데이터를 읽어서 표준 출력과 하나 이상의 다른 파일에 동시에 출력합니다. 이는 작업이
진행되고 있을 때, 중간 지점의 파이프라인에 있는 내용을 알고 싶을 때 유용합니다.

# 확장과 인용

#### echo

표준 출력상에 해당 텍스트 인자를 표시합니다.

### 경로명 확장

*기호 같이 와일드카드로 동작하는 방식을 **경로명 확장**이라고 합니다.

```shell

[me@linuxbox ~]$ echo D*
Dexktop Documents

```

### 틸드(~) 확장

```shell

[me@linuxbox ~]$ echo ~
/home/me

```
~ 기호 문자가 맨 앞에 있다면, 사용자의 홈 디렉토리 명을 나타냅니다.

### 산술 확장

> $((expression))

```shell

[me@linuxbox ~]$ echo $((2 + 2))
4

```

### 중괄호 확장

```shell

[me@linuxbox ~]$ echo Front-{A..C}-Back
Front-A-Back Front-B-Back Front-C-Back

```

중괄호에 의해 확장된 패턴은 프리앰블이라고 부르는 앞부분과 포스트스크립트라는 끝부분을 가집니다.

### 매개변수 확장

```shell

[me@linuxbox ~]$ echo $USER
me

```

```shell

[me@linuxbox ~]$ ls -l $(which cp)
-rwxr -xr -x 1 root root 71516 2012-12-05 08:58 /bin/cp

```

### 따옴표 활용

셀은 원하지 않는 확장을 선택적으로 감출 수 있도록 **따옴표 기호**를 활용하는 기능을 제공해줍니다.

**쌍따옴표 기호** 여부에 따른 차이 및 해결법
```shell

[me@linuxbox ~]$ ls -l two words.txt
ls: cannot access two: No such file or directory
ls: cannot access words.txt: No such file or directory

[me@linuxbox ~]$ ls -l "two words.txt"
-rw-rw-r-- 1 me me 18 2012-02-20 13:03 two words.txt
[me@linuxbox ~]$ mv "two words.txt" two_words.txt // 해결법

```

모든 확장을 숨겨야 한다면 **따옴표 기호**를 사용하면 됩니다.

```shell

[me@linuxbox ~]$ echo "text~/*.txt {a,b} $(echo foo) $((2 + 2)) $USER" 
text~/*.txt {a,b} foo 4 me
[me@linuxbox ~]$ echo 'text~/*.txt {a,b} $(echo foo) $((2 + 2)) $USER'
text~/*.txt {a,b} foo $(echo foo) $((2 + 2)) $USER

```

선택적으로 확장을 막거나 파일명에 있는 어떤 문자가 가지고 있는 특별한 의미를 없애고 싶을 때, 해당 문자 앞에 백슬래시를 추가하면 되는데,
이것을 **이스케이프 문자**라고 부릅니다.

# 고급 키보드 기법

### 커맨드라인 편집

#### 커서이동

커서 이동 명령어

| 키 | 실행 |
|:--:|:---:|
| CTRL-A | 줄 맨 앞으로 커서 이동 |
| CTRL-E | 줄 맨 끝으로 커서 이동 |
| CTRL-F | 다음 한 글자로 커서 이동. 오른쪽 화살표 키와 동일함 |
| CTRL-B | 이전 한 글자로 커서 이동. 왼쪽 화살표 키와 동일함 |
| ART-F | 다음 한 단어로 커서 이동 |
| ART-B | 이전 한 단어로 커서 이동 |
| CTRL-L | 화면을 지우고 커서를 왼쪽 최상단으로 이동. CLEAR 명령어와 동일함 |

#### 텍스트 수정

| 키 | 실행 |
|:--:|:---:|
| CTRL-D | 현재 커서 위치에 있는 글자 지우기 |
| CTRL-T | 현재 커서 위치에 있는 글자와 바로 앞 글자의 위치 바꾸기 |
| ART-T | 현재 커서 위치에 있는 단어와 바로 앞 단어의 위치 바꾸기 |
| ART-L | 현재 커서 위치에 있는 글자부터 그 단어 끝 부분까지 소문자로 바꾸기 |
| ART-U | 현재 커서 위치에 있는 글자부터 그 단어 끝 부분까지 대문자로 바꾸기 |

#### 텍스트 지우고 복사하기

| 키 | 실행 |
|:--:|:---:|
| CTRL-K | 현재 커서 위치로부터 그 줄 끝 부분까지 텍스트 지우기 |
| CTRL-U | 현재 커서 위치로부터 그 줄 처음 부분까지 텍스트 지우기 |
| ART-D | 현재 커서 위치에서부터 그 단어 끝 부분까지 텍스트 지우기 |
| ART-BACKSPACE | 현재 커서 위치에서부터 그 단어 앞부분까지 텍스트 삭제하기. 단, 커서가 단어 맨 앞에 위치하고 있다면 바로 앞 단어를 삭제함 |
| CTRL-Y | kill-ring에 있는 텍스트를 복사해서 현재 커서 위치에 삽입하기(잘라낸 데이터는 kill-ring이라고 하는 버퍼에 저장됩니다. |

### 자동 완성

명령어를 입력하는 동안 탭키를 누르면 자동 완성 기능이 작동합니다. 탭 키를 두번 입력하면 가능한 자동 완성 목록을 보여줍니다.

### 히스토리 활용

```shell

[me@linuxbox ~]$ history | grep /usr/bin

```

히스토리 확장

```shell

[me@linuxbox ~]$ !88

```
bash는 !88을 히스토리 목록에 있는 88번째 줄의 내용으로 확장시킬 것입니다.

히스토리 명령어

| 키 | 실행 |
|:--:|:---:|
| CTRL-P | 이전 히스토리 항목으로 이동. 위쪽 화살표키와 동일함. |
| CTRL-N | 다음 히스토리 항목으로 이동. 아래쪽 화살표키와 동일함. |
| ART-< | 히스토리 목록 처음으로 이동. |
| ART-> | 히스토리 목록 마지막으로 이동(현재 커맨드라인 기준). |
| CTRL-R | 역순 증분 검색. 현재 커맨드라인에서 히스토리 목록으로 증분 검색. |
| ART-P | 역순 검색. 증분 검색이 아님. 이 키 다음에, 검색 문자열을 입력한 후 검색이 실행되기 전에 엔터키를 누릅니다. |
| ART-N | 순방향 검색. 증분 검색 아님. |
| CTRL-O | 히스토리 목록에 있는 현재 항목을 실행하고 다음 항목으로 이동합니다. 히스토리 목록에 있는 순서대로 명령어를 재실행할 때 매우 편리함. |

증분 검색이란 명령어의 각 글가자 추가될 때마다 우리가 원하는 검색 결과를 골라서 보여주는 것입니다.

히스토리 확장 명령어

| 키 | 실행 |
|:--:|:---:|
| !! | 마지막 명령어를 반복하여 실행. 위쪽 화살표와 엔터키를 입력하는 것보다 아마 더 용이할 것입니다. |
| !number | 이 번호에 해당하는 항목을 실행. |
| !string | 이 문자열로 시작하는 가장 최근에 입력된 항목을 실행. |
| !?string | 이 문자열이 포함된 가장 최근에 입력된 항목을 실행. |

# 퍼미션


# 프로세스





























