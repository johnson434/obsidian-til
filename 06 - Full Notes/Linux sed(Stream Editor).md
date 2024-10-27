---
⭕첫 학습날: 2024-07-29
⭕과목: Linux
❤1일복습여부: true
🧡4일복습여부: true
💛7일복습여부: true
💚14일복습여부: true
🧠장기기억: false
복습: 추가 복습
🛑첫날: "✏첫날 : 2024/07/29"
🛑오늘: "⏰오늘 : 2024/10/27"
🛑첫학습후 몇일째?: 첫 학습 후 ❤90일째❤
🛑4일후: "🥉4일뒤 : 2024/08/02"
🛑7일후: "🥈7일뒤 : 2024/08/05"
🛑14일후: "🥇14일뒤 : 2024/08/12"
4일후: "@2024년 8월 2일"
4일후(text): 2024/08/02
7일후: "@2024년 8월 5일"
7일후(text): 2024/08/05
14일후: "@2024년 8월 12일"
14일후(text): 2024/08/12
오늘1: "@2024년 10월 27일 오후 2:02"
오늘2: 2024/10/27
첫학습날text: 2024/07/29
오늘과 첫학습날 사이: "90"
사이: "90"
"1일차복습여부1,0": "1"
"4일차복습여부1,0": "1"
"7일차복습여부1,0": "1"
"장기기억저장여부1,0": "0"
학습률: "0.6"
진행바: 🟩🟩🟩🟩🟩🟩⬜⬜⬜⬜ 60%
---
[[Linux]] [[Linux Tool]] 
### 단서 질문

- **sed란?**
    
    stream editor의 줄임말로 텍스트를 stream 형식으로 수정(edit)하는 기능을 말한다.
    
    데이터의 경우, Stream이란 형식으로 입출력에서 하나씩 요소가 나오는데 이러한 요소를 수정하는 것이다. 파일을 입력 받으면 파일은 데이터의 흐름 형식으로 입력을 받고 요소들을 수정하여 데이터의 흐름 형식으로 출력한다. 이걸 파일에 저장하거나 다시 스트림으로 받아서 수정할 수도 있다.
    

### 핵심 필기

- 전체 내용 접기
    
    [https://www.youtube.com/watch?v=EACe7aiGczw&ab_channel=DistroTube](https://www.youtube.com/watch?v=EACe7aiGczw&ab_channel=DistroTube)
    
    - 한 라인에 일치하는 첫번째 패턴만 바꾸기
        
        ```Bash
        sed 's/[검색 패턴]/[바뀔 패턴]/' <file_name >output_name
        ```
        
    - 일치하는 모든 패턴 제거
        
        ```Bash
        sed 's/[검색 패턴]/[바뀔 패턴]/g' <file_name >output_name
        sed /man/d 파일명 # man이 포함된 줄 삭제
        ```
        
    - 입력 받은 파일 수정하기
        
        ```Bash
        # i 옵션을 사용하면 가능하다(in place)
        # 입력과 출력 파일이 동일하므로 '<'를 통해 입력할 필요 없음. 단순 파일 명시만 하면됨.
        sed -i 's/[검색 패턴]/[바뀔 패턴]/' file_name
        ```
        
    - sed를 여러 번 사용할 때
        
        ```Bash
        # -e 옵션은 sed 명령어를 통한 출력 값을 보여줍니다.
        sed /man/p -e /girl/p # man과 girl이 들어있는 줄을 한 번 더 출력
        ```
        
    - 해당 조건에 맞는 부분만 출력
        
        ```Bash
        # p 옵션은 출력을 의미한다.
        # -n: 조건에 해당되는 줄만 출력
        sed -n '/^dd/p' file
        sed -n '/^dd/p' sed2cpoy
        ```
        

### 핵심 요약

- 핵심 요약 접기
    - 학습내용을 몇문장으로 압축하여 정리한다.

### 복습알림

- 
- 자동으로 핸드폰에 알림이 오도록 설정하고 싶으면 다음과 같이 한다.

> [!important]  
> 