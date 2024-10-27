---
⭕첫 학습날: 2024-06-19
⭕과목: DevOps
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: false
복습: 장기기억
🛑첫날: "✏첫날 : 2024/06/19"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤130일째❤
🛑4일후: "🥉4일뒤 : 2024/06/23"
🛑7일후: "🥈7일뒤 : 2024/06/26"
🛑14일후: "🥇14일뒤 : 2024/07/03"
4일후: "@2024년 6월 23일"
4일후(text): 2024/06/23
7일후: "@2024년 6월 26일"
7일후(text): 2024/06/26
14일후: "@2024년 7월 3일"
14일후(text): 2024/07/03
오늘1: "@2024년 10월 27일 오후 2:02"
오늘2: 2024/10/27
첫학습날text: 2024/06/19
오늘과 첫학습날 사이: "130"
사이: "130"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "0"
학습률: "0.6"
진행바: 🟩🟩🟩🟩🟩🟩⬜⬜⬜⬜ 60%
---
[[Linux]] [[Bash]]
### 단서 질문

- 쉘이란?
    
    리눅스 명령어를 실행하기 위한 인터프리터이자 환경
    
- 리눅스에서 연산하는 방법
    1. $(())
        1. c=$((a + b))
    2. `expr `
        1. c=`expr 1 + 2`
    3. let
        1. let a=1+2
- 문자열 대체
    1. 앞에 있는 문자를 대체하는 방법
        1. ${var\#pattern}: 하나만 대체한다.
        2. ${var#\#pattern}: 모든 패턴을 대체한다.
    2. 뒤에 있는 문자를 대체하는 방법
        1. ${var%pattern}: 하나만 대체한다.
        2. ${var%%pattern}: 모두 대체한다.

### 핵심 필기

- 전체 내용 접기
    
    # 핵심 요소
    
    - 명령어 대체 Command Substitution
        - $()
            - chmod +x $(id -u):
        - ``
            - chmod +x `id -u`
    - $(()): 산술 확장
    
    # 셔뱅(Shebang)
    
    어떤 쉘로 스크립트를 실행할지 명시하는 부분
    
    ```Ruby
    #! /bin/bash
    echo 'hello world'
    ```
    
    # 쉘 변수 선언
    
    - 변수는 대소문자를 구별
    - 변수는 숫자를 포함할 수 있지만, 숫자로 시작할 수 없다.
    - 변수에는 모든 값을 문자열로 저장한다.
    - 값을 사용할 때는 ‘$’를 사용한다. (ex: echo $name)
    - 값을 대입(삽입)할 때는 특수문자 ‘$’를 사용하지 않는다. (ex: data=mac)
    - 변수를 생성할 때는 ‘=’ 대입문자 앞뒤로 공백이 없어야 한다. (ex: data=”abcd”)
    
    ## 변수 타입 지정하기
    
    ```Bash
    #! /usr/bin/bash
    
    # 변수의 타입 지정하기
    
    echo ""
    echo "01.variable_type.sh"
    # 1. 상수형
    function readonly_test_function() {
      echo "declare를 통해 선언한 변수는 해당 변수가 속한 스코프에 속한다. 만약, 함수 내에 사용 되면 함수 변수가 된다."
    	declare -r readonly_variable="readonly_value"
    	echo "readonly_value=${readonly_variable}"
    }
    
    readonly const_variable="const_value"
    echo "readonly를 통해 선언한 변수는 Global Scope를 사용한다. 따라서, 전역 변수가 된다."
    echo "const_variable = ${const_variable}"
    
    readonly_test_function
    
    # 2. 정수형
    echo "==정수형 선언=="
    echo "declare -i integer_variable=4"
    declare -i integer_variable=4
    echo "integer_variable=${integer_variable}"
    
    # 3. 배열형
    echo "==배열형 선언=="
    echo "declare -a array_variable=(3,5,7)"
    declare -a array_variable=(3,5,7)
    echo "array_variable=${array_variable}"
    
    # 4. map형
    echo "==Map형 선언=="
    echo "declare -A map_variable"
    echo "map_variable[1]=1"
    declare -A map_variable
    map_variable[1]=1
    echo "map_variable[1]=${map_variable[1]}"
    
    # 5. 함수타입
    echo "==함수 타입=="
    echo "declare -f 함수명"
    
    # 6. 환경 변수 타입
    echo "==환경 변수 타입=="
    echo "declare -x 환경 변수 타입"
    declare -x environmental_variable=1
    ```
    
    1. 로컬 변수: local 키워드를 사용하면 된다.
    
    ```Bash
    #! /usr/bin/bash
    
    # 함수 내에서만 사용 가능하다.
    local local_variable='local_variable'
    echo "hello ${local_variable}" # {}가 있으나 없으나 $만으로 변수의 값을 넣어줄 수 있으나, 문자열을 붙여서 쓸려면 ${} 를 사용해야 한다.
    ```
    
    1. 전역 변수: 기본적으로 모든 변수는 전역 변수다.
    
    ```Bash
    #! /usr/bin/bash
    global_variable='hi'
    ```
    
    1. 환경 변수: export 키워드를 통해 자식 쉘 스크립트에서 사용이 가능하다.
    
    ```Bash
    #! /usr/bin/bash
    export environment_variable
    ./child_shell.sh
    ```
    
    ```Bash
    #! /usr/bin/bash
    echo $0 # child_shell.sh
    echo $environment_variable
    ```
    
    1. 예약 변수
    
    |변수|설명|
    |---|---|
    |HOME|사용자 홈 디렉터리|
    |PATH|실행 파일의 경로. chmod, mkdir 등의 명령어가 있는 /bin이나 /usr/bin 등|
    |LANG|프로그램 실행 시 지원되는 언어|
    |UID|사용자의 UID|
    |SHELL|사용자가 로그인 시 실행되는 셸|
    |USER|사용자의 계정 이름|
    |FUNCNAME|현재 실행되고 있는 함수 이름|
    |TERM|로그인 터미널|
    
    1. 매개 변수
    
    ![[Untitled 32.png]]
    
    |종류|설명|
    |---|---|
    |$0|실행된 셸 스크립트명|
    |$1..$n|스크립트에 넘겨진 매개변수|
    |$#|매개변수 개수|
    |$*|스크립트에 전달된 인자 전체를 하나의 변수에 저장하면 IFS 변수의 첫 번째 문자로 구분|
    |$@|$*와 동일한데 다른 점은 IFS 환경 변수를 사용하지 않는다.|
    |$!|실행을 위해 백그라운드로 보내진 마지막 프로그램 프로세스 번호|
    |$$|셸 스크립트의 PID|
    |$?|실행한 뒤의 반환 값(백그라운드 제외)|
    
    # 산술 연산
    
    1. expr
    2. let
    3. $(())
    
    ## expr
    
    - 역따옴표(`: 백틱)로 감싸준다.
    - 피연산자와 연산자 사이에 공백이 필요하다.(대입 연산자랑 반대네)
    - 우선 순위를 지정하기 위해 괄호를 사용하려면 \처리가 필요하다.(이스케이프용으로 붙이는듯)
    - 곱셉 문자 *는 \처리를 해줘야 한다.(정규식이랑 겹쳐서 그런듯)
    - 괄호로 우선순위 줄 때, 띄어쓰기 해야함.
        - 예시: \( 1 + 2 \) * 10
    
    ```Bash
    #!/bin/bash
    
    number1=10
    number2=20
    
    plus=`expr $number1 + $number2` 
    minus=`expr $number1 - $number2`
    mul=`expr $number1 \* $number2` # 곱셈에는 \* 를 이용한다.
    div=`expr $number1 / $number2`
    rem=`expr $number1 % $number2`
    
    echo "plus:     ${plus}"
    echo "minus:    ${minus}"
    echo "mul:      ${mul}"
    echo "div:      ${div}"
    echo "rem:      ${rem}"
    ```
    
    ## let
    
    - 연산자까지 다 붙여 써야함.
    
    ```Bash
    let result=1+2
    let result=1*2
    ```
    
    ### $(()) 연산자(개인적으로 제일 편한듯)
    
    ```Bash
    a=1
    b=2
    c=$((1 + 2))
    echo $c
    ```
    
    # 쉘 주석
    
    ```Bash
    <코드라인>
    : << "END"              #주석 시작
    echo "여기서부터 "
    echo "test_01"
    echo "test_02"
    echo "test_03"
    echo "test_04"
    echo "test_05"
    echo "test_06"
    echo "test_07"
    echo "여기까지 주석처리 됨"
    END                    #주석 끝
    
    echo "여기는 주석이 안되어 있어 출력 "
    출처: https://inpa.tistory.com/entry/LINUX-쉘-프로그래밍-핵심-문법-총정리\#thankYou [Inpa Dev 👨‍💻:티스토리]
    ```
    
    # 조건문
    
    - 중괄호를 안쓰므로 fi로 if문의 끝을 알려줘야 한다.
    - 대괄호([])엔 대괄호와 조건식 사이에 공백이 있어야 한다.
    
    ```Bash
    if [1 < 2] # 안된다. 대괄호와 식 사이에 띄어쓰기가 들어가야됨.
    
    if [ 1 < 2 ]
    then
    else
    fi
    
    if [ 1 < 2 ]; then # 가독성을 위해서 if then을 같은 줄에 쓰려면 세미콜론을 써야한다.
    
    elif [ 1 < 3 ]
    	echo "hi"
    else
    	echo "hi"
    fi
    ```
    
    ## 비교 연산
    
    ```Bash
    문자1 = 문자2             # 문자1 과 문자2가 일치 (sql같이 = 하나만 써도 일치로 인식)
    문자1 == 문자2            # 문자1 과 문자2가 일치
    문자1 != 문자2            # 문자1 과 문자2가 일치하지 않음
    -z 문자                   # 문자가 null 이면 참
    -n 문자                   # 문자가 null 이 아니면 참
    문자 == 패턴              # 문자열이 패턴과 일치
    문자 != 패턴              # 문자열이 패턴과 일치하지 않음
    
    값1 -eq 값2             # 값이 같음(equal)
    값1 -ne 값2             # 값이 같지 않음(not equal)
    값1 -lt 값2             # 값1이 값2보다 작음(less than)
    값1 -le 값2             # 값1이 값2보다 작거나 같음(less or equal)
    값1 -gt 값2             # 값1이 값2보다 큼(greater than)
    값1 -ge 값2             # 값1이 값2보다 크거나 같음(greater or equal)
    ```
    
    ```Bash
    # 한줄로 작성
    if [ ${num1} -lt ${num2} ]; then echo "yes"; fi
    
    # 이중 소괄호를 쓰면 조건문을 문자 대신 기호로 표현 가능하다. 단, 소괄호 안에 따옴표 쓰면 안된다.
    if (( ${num1} < ${num2} )); then
        echo "yes"
    fi
    ```
    
    > [!important]  
    > 이중 괄호 (( expression ))expression 에는 수식이나 비교 표현식이 들어갈 수 있다.  
      
    !         논리 부정-  
    ~        비트 부정  
    **        지수화  
    <<      비트 왼쪽 쉬프트  
    >>      비트 오른쪽 쉬프트  
    &        비트 단위AND  
    |          비트 단위 OR  
    &&      논리 AND  
    ||         논리 OR  
    num++   후위증가  
    num--     후위감소++  
    num       전위증가  
    --num     전위감소  
    
      
    
    ## 파일 검사
    
    ![[Untitled 1 18.png]]
    
    > [!important]  
    > 블록 디바이스(Block Device)는 HDD나 SDD와 같은 저장 장치를 말합니다. 블록 단위로 데이터를 저장하는 장치들을 말합니다.  
      
    > [!important]  
    > 캐릭터 디바이스(Character Device)는 키보드, 마우스, 모니터, 프린터 등의 장치를 말합니다. byte 단위로 데이터를 전송합니다. I/O 전송속도가 다소 느릴 수도 있으나, 어플리케이션단에서 버퍼링을 제어하므로, 성능에 따라 차이가 있을 수 있습니다.  
    
    ## 논리 연산
    
    ```Bash
    조건1 -a 조건2         # AND
    조건1 -o 조건2         # OR
    조건1 && 조건2         # 양쪽 다 성립
    조건1 || 조건2         # 한쪽 또는 양쪽다 성립
    !조건                  # 조건이 성립하지 않음
    true                   # 조건이 언제나 성립
    false                  # 조건이 언제나 성립하지 않음
    ```
    
    ```Bash
    f [ -f ${file1} -a -f ${file2} ]; then
        echo 'file1과 file2는 모두 파일입니다.'
    else
        echo 'file1과 file2가 모두 파일인 것은 아닙니다.'
    fi
    
    
    if [ -f ${a} -a -d ${b} ]; then
        echo "a는 파일이고 b는 디렉토리"
    fi
    
    if [ ${VALUE} -gt 5 -a ${VALUE} -lt 15 ] ; then
    	echo "VALUE is greater than 5 and less than 15!"
    fi
    
    # 둘이 같은 문장이다.
    if [ ${VALUE} -gt 5 ] && [ ${VALUE} -lt 15 ] ; then
    	echo "VALUE is greater than 5 and less than 15!"
    fi
    
    # 대괄호 두개를 써서 표현할 수 도 있다.
    if [[ ${VALUE} -gt 5 && ${VALUE} -lt 15 ]] ; then
    	echo "VALUE is greater than 5 and less than 15!"
    fi
    
    # AND 
    if [ ${string1} == ${string2} ] && [ ${string3} == ${string4} ] ;
    then
    
    # OR 
    if [ ${string1} == ${string2} ] || [ ${string3} == ${string4} ];
    then 
    
    # 다중 조건 
    if [[ ${string1} == ${string2} || ${string3} == ${string4} ]] && [ ${string5} == ${string6} ];
    then
    ```
    
    ## if elif else
    
    ```Bash
    #!/bin/bash
    
    num1="10"
    num2="10"
    
    if [ ${num1} -lt ${num2} ]; then # "-lt", A가 B보다 작으면 True
        echo "yes"
    elif [ ${num1} -eq ${num2} ]; then # "-eq", A와 B가 서로 같으면 True
        echo "bbb"
    else
        echo "no"
    fi
    
    
    # 이중 소괄호를 쓰면 논리연산자 기호 사용 가능
    if (( ${num1} < ${num2} )); then
        echo "yes"
    elif (( ${num1} == ${num2} )); then
        echo "bbb"
    else
        echo "no"
    fi
    
    
    # 한줄 작성
    if [ ${num1} -lt ${num2} ]; then echo "yes"; elif [ ${num1} -eq ${num2} ]; then echo "bbb";  else echo "no"; fi
    ```
    
    ## case
    
    ```Bash
    case ${var} in
        "linux") echo "리눅스" ;; # 변수var값이 linux라면 실행 
        "unix") echo "유닉스" ;;    
        "windows") echo "윈도우즈" ;;    
        "MacOS") echo "맥OS" ;;    
        *) echo "머야" ;; # default 부분
    esac
    
    COUNTRY=korea
    
    case $COUNTRY in
      "korea"|"japan"|"china") # or 연산도 가능하다
        echo "$COUNTRY is Asia"
        ;;
      "USA"|"Canada"|"Mexico")
        echo "$COUNTRY is Ameria"
        ;;
      * )
        echo "I don't know where is $COUNTRY"
        ;;
    esac
    
    date=210610 # 21년 6월 10일
    
    case $date in # ? 는 임의의 한문자
      ??03?? | ??04?? | ??05??) echo 봄이구나~! ;; # 3월이거나 4월이거나 5월일 때
      ??06?? | ??07?? | ??08??) echo 여름이구나~! ;;
      ??09?? | ??10?? | ??11??) echo 가을이구나~! ;;
      ??12?? | ??01?? | ??02??) echo 겨울이구나~! ;;
      *) echo 아 일하기 싫다 ;;
    esac
    
    str="abc"
    
    case $str in
      a*) # a이후 임의의 어떠한 문자라도 오면 일치 (0개~여러개)
        echo "$str starts with a"
        ;;
      a?) # a이후 반드시 임의의 하나의 문자가 오면 일치
        echo "$str starts with a and has two words"
        ;;
      a[bc]) # a이후 b나 c가 오면 일치
        echo "$str starts with a and then followed by b or c "
        ;;
      * ) # default
        echo "I don't know where is $COUNTRY"
        ;;
     esac
    ```
    
    # 반복문
    
    ## for문
    
    ```Bash
    #!/bin/bash
    
    # 루프 돌 데이터에 띄어쓰기가 있으면 각각 돌음
    for x in 1 2 3 4 5
    do
    	echo "${x}"
    done
    
    
    # 변수를 사용한 반복문
    data="1 2 3 4 5"
    for x in $data
    do
    	echo ${x}
    done
    
    
    # 배열을 사용한 반복문
    arr=(1 2 3 4 5)
    for i in "${arr[@]}" # arr[@] : 배열 전체 출력
    do
    	echo "${i}"
    done
    
    
    # sequence를 통한 for문. seq라는 프로세스가 순서대로 숫자를 출력해 주는 역할을 bash에 사용한 것이다.
    for num in `seq 1 5`
    do
      echo $num
    done
    
    
    # range를 사용한 반복문. {..} 중괄호와 점 두개를 쓰면 range처리가 된다.
    for x in {1..5}
    do
    	echo ${x}
    done
    
    for file in `ls`; do
    	echo $file
    done
    ```
    
    ## while문
    
    ```Bash
    count=0
    while (($count <= 5))
    do
    	count=$(($count + 1))
    done
    
    # 한줄 입력
    a=0
    while ((++a <= 10)); do echo $a; done
    ```
    
    # 배열
    
    **배열 추가하기**
    
    ```Bash
    array=(1 2 3 4)
    array+=(5)
    
    array[${\#array[@]}]=6
    ```
    
    배열 삭제하기
    
    ```Bash
    arr=(1 2 3)
    remove_element=(3)
    
    arr=( "${arr[@]/$remove_element}" ) # 배열 1 2 3 에서 / 3을 없앰
    
    echo ${arr[@]} # > 1 2
    
    arr=("abc" "def" "defghi")
    
    # 단, unset을 권장한다.
    unset arr[1] # 배열 특정 인덱스 요소 삭제
    # 터미널에서 실행 시엔 배열 인덱스를 땡긴다.
    # 셸 스크립트에서 실행 시엔 배열 인덱스를 안 땡김.
    
    echo ${arr[@]} > # abc defghi
    
    unset array # 배열 전체 지우기
    ```
    
    # Map
    
    ```Bash
    #! /usr/bin/bash
    echo
    echo "06.map.sh"
    declare -A map=(['key1']='value1')
    map['key2']='value2'
    map['key3']='value3'
    
    # key 출력
    echo ${!map[@]}
    # value 출력
    echo ${map[@]}
    
    echo
    for key in ${!map[@]}; do
    	echo "key: $key"
    	echo "value: ${map[$key]}"
    done
    ```
    
    # 함수
    
    ```Bash
    function func1() {
    	first_argument=$1
    	all_argument=$@
    }
    
    func1 1
    array=(1 2 3)
    func1 ${array[@]}
    
    # name reference
    function func2() {
    	declare -n passed_array=$1
    }
    
    func2 array
    ```
    
    # 명령어 종료 상태 코드
    
    ![[Untitled 2 16.png]]
    
    ```Bash
    exit 16
    exit 0
    exit 1
    
    echo "exit code: $?"
    ```
    
    # 명령어 대체
    
    - $(): command substiton으로 괄호 안에 내용을 명령어로 인식하고 실행 후 결과값을 반환한다.
    - ``: 위와 동일하게 내용을 실행하고 반환한다.
    
    # 문자열 대체
    
    ```Bash
    # var의 값이 null이면 word를 반환
    # var의 값이 null이 아니면 var을 반환
    ${var:-word}
    
    # var의 값이 null이면 word를 반환하고 var에 word를 대입
    # var의 값이 null이 아니면 ar을 반환
    ${var:=word}
    
    # var의 값이 null이면 null을 반환
    # var의 값이 null이 아니면 word의 값을 반환
    ${var:+word}
    
    # var의 값이 null이면 에러 메시지인 word를 출력하고 쉘 스크립트를 종료
    # var의 값이 null이 아니면 var의 값을 반환
    ${var:?word}
    
    ## 패턴 도입
    
    # 끝에서부터 word와 패턴이 일치하는 var의 첫번째 일치 부분을 제거하고 반환합니다.
    ${var%pattern}
    # 끝에서부터 word와 패턴이 일치하는 var의 최대 부분을 제거하고 나머지를 반환한다.
    ${var%%pattern}
    # 처음부터 word와 패턴이 일치하는 var의 최소 부분을 제거하고 나머지 부분을 반환
    ${var\#pattern}
    # 처음부터 word와 패턴이 일치하는 var의 최대 부분을 제거하고 나머지 부분을 반환
    ${var#\#pattern}
    ```
    
    ```Bash
    #!/bin/bash
    
    # var not exists
    unset var1
    echo ${var1:-string2}
    
    # var exists
    var1=string1
    echo ${var1:-string2}
    
    
    var1=/var/log/apt
    echo ${var1#*/}
    
    echo ${var1##*/}
    
    
    var2=/var/log/apt/log/ifconfig.cfg
    echo ${var2%log*}
    
    echo ${var2%%log*}
    
    $ ./script.sh
    string2
    string1
    var/log/apt
    apt
    /var/log/apt/
    /var/
    ```
    

### 핵심 요약

- 핵심 요약 접기
    
    **명령어 대체**
    
    - $()
    - ``
    
    조건문
    
    - if then fi
    - case
    
    반복문
    
    - for do done
    - while do done

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 