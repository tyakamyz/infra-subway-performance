<p align="center">
    <img width="200px;" src="https://raw.githubusercontent.com/woowacourse/atdd-subway-admin-frontend/master/images/main_logo.png"/>
</p>
<p align="center">
  <img alt="npm" src="https://img.shields.io/badge/npm-%3E%3D%205.5.0-blue">
  <img alt="node" src="https://img.shields.io/badge/node-%3E%3D%209.3.0-blue">
  <a href="https://edu.nextstep.camp/c/R89PYi5H" alt="nextstep atdd">
    <img alt="Website" src="https://img.shields.io/website?url=https%3A%2F%2Fedu.nextstep.camp%2Fc%2FR89PYi5H">
  </a>
  <img alt="GitHub" src="https://img.shields.io/github/license/next-step/atdd-subway-service">
</p>

<br>

# 인프라공방 샘플 서비스 - 지하철 노선도

<br>

## 🚀 Getting Started

### Install
#### npm 설치
```
cd frontend
npm install
```
> `frontend` 디렉토리에서 수행해야 합니다.

### Usage
#### webpack server 구동
```
npm run dev
```
#### application 구동
```
./gradlew clean build
```
<br>
---
## 🚀 1단계 - 화면 응답 개선하기
### 요구사항
- 저장소를 활용하여 아래 요구사항을 해결합니다.
- README 에 있는 질문에 답을 추가한 후 PR을 보내고 리뷰요청을 합니다.
- [x] 부하테스트 각 시나리오의 요청시간을 목푯값 이하로 개선 
  - 개선 전 / 후를 직접 계측하여 확인

## 🚀 2단계 - 스케일 아웃 (with ASG)
### 요구사항
- [x] springboot에 HTTP Cache, gzip 설정하기
- [x] Launch Template 작성하기
- [x] Auto Scaling Group 생성하기
- [x] Smoke, Load, Stress 테스트 후 결과를 기록

## 🚀 3단계 - 쿼리 최적화
### 요구사항
- [x] 활동중인(Active) 부서의 현재 부서관리자(manager) 중 연봉 상위 5위안에 드는 사람들이 최근에 각 지역별로 언제 퇴실(O)했는지 조회해보세요.
    - (사원번호, 이름, 연봉, 직급명, 지역, 입출입구분, 입출입시간)
- [x] 인덱스 설정을 추가하지 않고 1s 이하로 반환합니다.
    - M1의 경우엔 시간 제약사항을 달성하기 어렵습니다. 2배를 기준으로 해보시고 어렵다면, 일단 리뷰요청 부탁드려요
    - 급여 테이블의 사용여부 필드는 사용하지 않습니다. 현재 근무중인지 여부는 종료일자 필드로 판단해주세요.

## 🚀 4단계 - 인덱스 설계
### 요구사항
- [x] 주어진 데이터셋을 활용하여 아래 조회 결과를 100ms 이하로 반환
    - [x] Coding as a Hobby 와 같은 결과를 반환하세요.
    - [x] 프로그래머별로 해당하는 병원 이름을 반환하세요. (covid.id, hospital.name)
    - [x] 프로그래밍이 취미인 학생 혹은 주니어(0-2년)들이 다닌 병원 이름을 반환하고 user.id 기준으로 정렬하세요. (covid.id, hospital.name, user.Hobby, user.DevType, user.YearsCoding)
    - [x] 서울대병원에 다닌 20대 India 환자들을 병원에 머문 기간별로 집계하세요. (covid.Stay)
    - [x] 서울대병원에 다닌 30대 환자들을 운동 횟수별로 집계하세요. (user.Exercise)

## 미션

* 미션 진행 후에 아래 질문의 답을 작성하여 PR을 보내주세요.


### 1단계 - 화면 응답 개선하기
1. 성능 개선 결과를 공유해주세요 (Smoke, Load, Stress 테스트 결과)
   - 성능 개선 전
     - smoke(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/1_before/smoke_K6.png)
     - load(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/1_before/load_K6.png)
     - stress(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/1_before/stress_K6.png)
   - ngnix proxy 개선 후
     - smoke(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/2_proxy/smoke_K6.png)
     - load(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/2_proxy/load_K6.png)
     - stress(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/2_proxy/stress_K6.png)
   - was 개선 후
     - smoke(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/3_was/smoke_K6.png)
     - load(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/3_was/load_K6.png)
     - stress(https://github.com/tyakamyz/infra-subway-performance/blob/step1/performance/3_was/stress_K6.png)
     
2. 어떤 부분을 개선해보셨나요? 과정을 설명해주세요
   - gzip 압축
   - cache 설정
   - TLS, HTTP/2 설정
   - Redis - Spring Data Cache

---

### 2단계 - 스케일 아웃

1. Launch Template 링크를 공유해주세요.
   - https://ap-northeast-2.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-2#LaunchTemplateDetails:launchTemplateId=lt-01796a4cbdd222dce
   
2. cpu 부하 실행 후 EC2 추가생성 결과를 공유해주세요. (Cloudwatch 캡쳐)
![img.png](./performance/step2/instances.png)

3. 성능 개선 결과를 공유해주세요 (Smoke, Load, Stress 테스트 결과)
   - smoke (https://github.com/tyakamyz/infra-subway-performance/blob/step2/performance/step2/smoke_K6.png)
   - load (https://github.com/tyakamyz/infra-subway-performance/blob/step2/performance/step2/load_K6.png)
   - stress (https://github.com/tyakamyz/infra-subway-performance/blob/step2/performance/step2/stress_K6.png)

---

### 1단계 - 쿼리 최적화

1. 인덱스 설정을 추가하지 않고 아래 요구사항에 대해 1s 이하(M1의 경우 2s)로 반환하도록 쿼리를 작성하세요.

- 활동중인(Active) 부서의 현재 부서관리자 중 연봉 상위 5위안에 드는 사람들이 최근에 각 지역별로 언제 퇴실했는지 조회해보세요. (사원번호, 이름, 연봉, 직급명, 지역, 입출입구분, 입출입시간)

```sql
select
    T.id as 사원번호,
    T.name as 이름,
    T.annual_income as 연봉,
    T.position_name as 직급명,
    R.region as 지역,
    R.record_symbol as 입출입구분,
    R.time as 입출입시간
from record R join
     (select
          E.id,
          concat(E.last_name, ' ', E.first_name) as name,
          S.annual_income,
          P.position_name
      from department D
               join manager M
                    on D.id = M.department_id
                        and upper(D.note) = 'ACTIVE'
               join employee E
                    on E.id = M.employee_id
               join position P
                    on P.id = M.employee_id
                        and P.position_name = 'Manager'
                        and P.end_date = '9999-01-01'
               join salary S
                    on S.id = M.employee_id
                        and S.end_date = '9999-01-01'
      ORDER BY S.annual_income DESC
          limit 5
     ) as T
     on R.employee_id = T.id
         and R.record_symbol = 'O';
```
![img.png](./performance/step3/result.png)

---

### 2단계 - 인덱스 설계

1. 인덱스 적용해보기 실습을 진행해본 과정을 공유해주세요
```sql
/* 1. Coding as a Hobby 와 같은 결과를 반환하세요. */
select hobby, concat(count(*) / (select count(*) from programmer) * 100,' %') as result
from programmer
group by hobby;
```
![img.png](./performance/step4/1_execution_plan.png)
- 0.031 sec / 0.000 sec
- programmer
    - id: PK 지정
    - hobby: index 생성

```sql
/* 2. 프로그래머별로 해당하는 병원 이름을 반환하세요. (covid.id, hospital.name) */
select C.id, H.name
from covid C
         join programmer P
              on P.id = C.programmer_id
         join hospital H
              on C.hospital_id = H.id;
```
![img.png](./performance/step4/2_execution_plan.png)
- 0.015 sec / 0.000 sec
- covid
    - id: PK 지정
    - programmer_id: unique 지정
    - hospital_id: index 생성
- programmer
    - id: PK 지정 (이전 sql 미션에서 지정)
- hospital
    - id: PK 지정
    - name: unique 지정

```sql
/* 3. 프로그래밍이 취미인 학생 혹은 주니어(0-2년)들이 다닌 병원 이름을 반환하고 user.id 기준으로 정렬하세요. 
(covid.id, hospital.name, user.Hobby, user.DevType, user.YearsCoding) */
select CH.id, CH.name, P.hobby, P.dev_type, P.Years_coding
from
    (
        select C.id, C.programmer_id, H.name
        from covid C
            join hospital H
              on C.hospital_id = H.id
    ) CH join
    (
        select P.id, P.hobby, P.dev_type, P.Years_coding
        from programmer P
        where P.hobby = 'Yes'
        and (P.student like 'Yes%' or P.years_coding = '0-2 years')
    ) P
    on CH.programmer_id = P.id
order by P.id;
```
![img.png](./performance/step4/3_execution_plan.png)
- 0.015 sec / 0.000 sec
- covid
    - id: PK 지정 (이전 sql 미션에서 지정)
    - programmer_id: unique 지정 (이전 sql 미션에서 지정)
- hospital
    - id: PK 지정 (이전 sql 미션에서 지정)
    - name: unique 지정 (이전 sql 미션에서 지정)
- programmer
    - id: PK 지정 (이전 sql 미션에 서 지정)
    - hobby: index 생성 (이전 sql 미션에서 지정)

```sql
/* 4. 서울대병원에 다닌 20대 India 환자들을 병원에 머문 기간별로 집계하세요. (covid.Stay) */
select C.stay, count(*)
from covid C
         join hospital H
           on C.hospital_id = H.id
          and H.name = '서울대병원'
         join programmer P
           on C.programmer_id = P.id
          and P.country = 'India'
group by C.stay;
```
![img.png](./performance/step4/4_execution_plan.png)
- 0.047 sec / 0.000 sec
- covid
    - id: PK 지정 (이전 sql 미션에서 지정)
    - hospital_id: index 생성 (이전 sql 미션에 서 지정)
    - programmer_id: unique 지정 (이전 sql 미션에 서 지정)
- hospital
    - id: PK 지정 (이전 sql 미션에서 지정)
    - name: unique 지정 (이전 sql 미션에서 지정)
- programmer
    - id: PK 지정 (이전 sql 미션에 서 지정)

```sql
/* 5. 서울대병원에 다닌 30대 환자들을 운동 횟수별로 집계하세요. (user.Exercise) */
select P.exercise, count(*)
from covid C
    join (
        select H.id, H.name
        from hospital H
        where H.name = '서울대병원'
    ) H
      on C.hospital_id = H.id
    join programmer P
      on C.programmer_id = P.id
    join (
        select M.id
        from member M
        where M.age between 30 and 39
    ) M
      on P.id = M.id
group by P.exercise;
```
![img.png](./performance/step4/5_execution_plan.png)
- 0.047 sec / 0.000 sec
- covid
    - id: PK 지정 (이전 sql 미션에서 지정)
    - hospital_id: index 생성 (이전 sql 미션에 서 지정)
    - programmer_id: unique 지정 (이전 sql 미션에 서 지정)
- programmer
    - id: PK 지정 (이전 sql 미션에 서 지정)
- hospital
    - id: PK 지정 (이전 sql 미션에서 지정)
    - name: unique 지정 (이전 sql 미션에서 지정)
- member
    - id: PK 지정 (이전 sql 미션에서 지정)
    - age: index 생성 (이전 sql 미션에서 지정)

#### 1~6 최종 결과 캡처
- 전체 결과
  - ![img.png](./performance/step4/result.png)
- 2번 문제 재캡처
  - ![img.png](./performance/step4/result_Q2.png)

---

### 추가 미션

1. 페이징 쿼리를 적용한 API endpoint를 알려주세요
