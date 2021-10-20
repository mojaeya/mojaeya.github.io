---
layout: post
title: "[백준/Node.js] 4344번 평균은 넘겠지"
category: Algorithm
tags: [git, baekjoon]
comments: true
---

## 문제
대학생 새내기들의 90%는 자신이 반에서 평균은 넘는다고 생각한다. 당신은 그들에게 슬픈 진실을 알려줘야 한다.

## 입력
첫째 줄에는 테스트 케이스의 개수 C가 주어진다.

둘째 줄부터 각 테스트 케이스마다 학생의 수 N(1 ≤ N ≤ 1000, N은 정수)이 첫 수로 주어지고, 이어서 N명의 점수가 주어진다. 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다.

## 출력
각 케이스마다 한 줄씩 평균을 넘는 학생들의 비율을 반올림하여 소수점 셋째 자리까지 출력한다.

## CODE
```javascript
const readline = require('readline')
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
})

let input = []

rl.on('line', function(line){
    input.push(line)
})
  .on('close', function(){
    for(let i=1; i<=input[0]; i++){
        const score = input[i].split(" ").map(Number) // 점수
        const stdNum = score[0] // 학생 수

        let sum = score.reduce((prev, curr) => { // 점수의 총합 : reduce 메서드 활용
            return prev + curr
        },-stdNum)  // 초기값은 학생 수이기 때문에 -학생수로 지정

        let avg = sum / stdNum // 평균

        let count = 0
        for(let j=1; j<=stdNum; j++) {
            if(score[j] > avg) { // 학생의 점수가 해당 케이스의 평균을 넘는 경우
                count++
            }
        }
        const overAvgR = (count / stdNum) * 100  // 평균을 넘는 학생들의 비율
        console.log(overAvgR.toFixed(3) + "%") // 소수점 자리수 지정 자르기 : toFixed()
    }

    process.exit()
})
```
## Comment
- reduce 메서드 : 배열의 첫번째 요소부터 마지막 요소까지의 합성곱 처리를 한다.

- <mark style='background-color: #ffdce0'> 합섭 곱 처리란? </mark>   
배열 요소 하나를 함수로 처리한 후에 그 반환값을 다음 번 요소를 처리할 때 함수의 입력 값으로 사용하는 처리 방법
 
- initial(초기값) 지정함 : prev는 initial의 값, curr은 배열의 첫번째 요소, index는 0
- initial(초기값) 지정안함 : prev는 배열의 첫번째 요소 값, curr은 배열의 두번째 요소 값, index는 1

// 10장 배열의 메서드 링크 추가하기 

<br>
<br>
<br>

**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://laycoder.tistory.com/184](https://laycoder.tistory.com/184)