
## 목차

- [프로젝트 배경](#프로젝트-배경)
- [목표](#목표)
- [요구사항](#요구사항)
- [Stack](#stack)
- [Database](#database)
- [UML](#uml)
- [Getting Started](#getting-started)
- [API List](#api-list)
- [구현](#구현)
  - [메뉴 신규 등록 - 피주문자](#메뉴-신규-등록---피주문자)
    - [요구사항](#요구사항)
    - [구현](#구현-1)
  - [메뉴 수정 / 삭제 - 피주문자](#메뉴-수정--삭제---피주문자)
    - [요구사항](#요구사항-1)
    - [구현 - 기존 메뉴 수정](#구현---기존-메뉴-수정)
    - [구현 - 기존 메뉴 삭제](#구현---기존-메뉴-삭제)
  - [메뉴 리스트 출력 조회 - 주문자](#메뉴-리스트-출력-조회---주문자)
    - [요구사항](#요구사항-2)
    - [구현 - 추천 메뉴 조회](#구현---추천-메뉴-조회)
    - [구현 - 주문순 조회](#구현---주문순-조회)
    - [구현 - 최신순 조회](#구현---최신순-조회)
    - [구현 - 평점순 조회](#구현---평점순-조회)
  - [메뉴별 평점 및 리뷰 조회 - 주문자](#메뉴별-평점-및-리뷰-조회---주문자)
    - [요구사항](#요구사항-3)
    - [구현](#구현-2)
  - [메뉴별 평점 작성 - 주문자](#메뉴별-평점-작성---주문자)
    - [요구사항](#요구사항-4)
    - [구현](#구현-3)
  - [주문 - 주문자](#주문---주문자)
    - [요구사항](#요구사항-5)
    - [구현](#구현-4)
  - [주문 변경 - 주문자](#주문-변경---주문자)
    - [요구사항](#요구사항-6)
    - [구현 - 메뉴 추가 (정상 추가 가능)](#구현---메뉴-추가-정상-추가-가능)
    - [구현 - 메뉴 추가 시 배달 중 일 경우(신규 주문으로 전환)](#구현---메뉴-추가-시-배달-중-일-경우신규-주문으로-전환)
    - [구현 - 메뉴 변경 시 상태가 조리중 배달 중 일경우](#구현---메뉴-변경-시-상태가-조리중-배달-중-일경우)
  - [주문 내역 조회 - 주문자](#주문-내역-조회---주문자)
    - [요구사항](#요구사항-7)
    - [구현 - 현재 주문내역 리스트 가져오기(배달완료가 아직 안된 목록)](#구현---현재-주문내역-리스트-가져오기배달완료가-아직-안된-목록)
    - [구현 - 과거 주문내역 리스트 가져오기(status code: 7 배달완료된 목록)](#구현---과거-주문내역-리스트-가져오기status-code-7-배달완료된-목록)
  - [주문 상태 조회 - 피주문자](#주문-상태-조회---피주문자)
    - [요구사항](#요구사항-8)
    - [구현 - 현재 주문내역 리스트 조회(주문접수가 완료된 것)](#구현---현재-주문내역-리스트-조회주문접수가-완료된-것)
    - [구현 - 각 메뉴별 상태 변경](#구현---각-메뉴별-상태-변경)
  - [Contact](#contact)


## 프로젝트 배경
언텍트 시대에 급증하고 있는 온라인 주문 시스템은 이미 생활전반에 그 영향을 끼치고 있는 상황에, 가깝게는 배달어플, 매장에는 키오스크, 식당에는 패드를 이용한 메뉴 주문까지 그 사용범위가 점점 확대되어 가고 있습니다. 이런 시대에 해당 시스템을 이해, 경험하고 각 단계별 프로세스를 이해하여 구현함으로써 서비스 구축에 경험을 쌓고, golang의 이해를 돕습니다.

학습자는 주문자/피주문자의 역할에서 필수적인 기능을 도출, 구현합니다.
학습자는 해당 시스템에 대해 요구사항을 접수하고 주문자와 피주문자 입장에서 필요한 기능을 도출하여, 기능을 확장하고 주문 서비스를 원할하게 지원할수 있는 기능을 구현합니다.
주문자는 신뢰있는 주문과 배달까지를 원합니다. 또, 피주문자는 주문내역을 관리하고 원할한 서비스가 제공되어야 합니다.

## 목표

- gin-gonic framework를 사용하여 온라인 주문 시스템 API Server를 개발합니다.
- 온라인 주문 시스템에 관련한 데이터베이스 document를 직접 설계합니다.
- 주문자, 피주문자 CRUD API를 개발합니다.
- mongodb와 연동하여 실제 데이터베이스에 데이터가 저장될 수 있게 합니다.
- 디버깅을 위한 로그 출력이 가능하게 구성합니다.
- 스웨거를 이용해 API 문서화를 합니다.
- toml을 이용해 설정 파일을 구성합니다.

## 요구사항

**메뉴 신규 등록 - 피주문자**

- API | 신규 메뉴 등록
    - 사업장에서 신규 메뉴 관련 정보를 등록하는 과정(ex. 메뉴 이름, 주문가능여부, 한정수량, 원산지, 가격, 맵기정도, etc)
    - 성공 여부를 리턴

**메뉴 수정 / 삭제 - 피주문자**

- API | 기존 메뉴 수정/삭제
    - 사업장에서 기존의 메뉴 정보 변경기능(ex. 가격변경, 원산지 변경, soldout)
    - 메뉴 삭제시, 실제 데이터 백업이나 뷰플래그를 이용한 안보임 처리
    - 금일 추천 메뉴 설정 변경, 리스트 출력
    - 성공 여부를 리턴

**메뉴 리스트 출력 조회 - 주문자**

- API | 메뉴 리스트 조회 및 정렬(추천/평점/주문수/최신)
    - 각 카테고리별 sort 리스트 출력(ex. order by 추천, 평점, 재주문수, 최신)
    - 결과 5~10여개 임의 생성 출력, sorting 여부 확인

**메뉴별 평점 및 리뷰 조회 - 주문자**

- API | 개별 메뉴별 평점 및 리뷰 보기
    - UI에서 메뉴 리스트에서 상기 리스트 출력에 따라 개별 메뉴를 선택했다고 가정
    - 해당 메뉴 선택시 메뉴에 따른 평점 및 리뷰 데이터 리턴

**메뉴별 평점 작성 - 주문자**

- API | 과거 주문 내역 중, 평점 및 리뷰 작성
    - 해당 주문내역을 기준, 평점 정보, 리뷰 스트링을 입력받아 과거 주문내역 업데이트 저장
    - 성공여부 리턴

**주문 - 주문자**

- API | UI에서 메뉴 리스트에서 해당 메뉴 선택, 주문 요청 및 초기상태 저장
    - 주문정보를 입력받아 주문 저장(ex. 선택 메뉴 정보, 전화번호, 주소등 정보를 입력받아 DB 저장)
    - 주문 내역 초기상태 저장
    - 금일 주문 받은 일련번호-주문번호 리턴

**주문 변경 - 주문자**

- API | 메뉴 변경 및 추가
    - 추가시 상태조회 후 `배달중`일 경우 실패 알림
        - 성공 실패 알림, 실패시 신규주문으로 전환
    - 변경시 상태가 `조리중`, `배달중`일 경우 확인
        - 성공 실패 알림

**주문 내역 조회 - 주문자**

- API | 주문내역 조회
    - 현재 주문내역 리스트 및 상태 조회 - 하기 주문 상태 조회에서도 사용
        - ex. 접수중/조리중/배달중 etc
        - 없으면 null 리턴
    - 과거 주문내역 리스트 최신순으로 출력
        - 없으면 null 리턴

**주문 상태 조회 - 피주문자**

- API | 현재 주문내역 리스트 조회
- API | 각 메뉴별 상태 변경-사업장
    - ex. 상태 : 접수중/접수취소/추가접수/접수-조리중/배달중/배달완료 등을 이용 상태 저장
    - 각 단계별 사업장에서 상태 업데이트
        - 접수중 → 접수 or 접수취소 → 조리중 or 추가주문 → 배달중
        - 성공여부 리턴


# Stack
___

- go
- gin-gonic
- swagger
- mongoDB

# Database

![Project 3 (1)](https://user-images.githubusercontent.com/20445415/210943436-107dbc57-9527-4753-aefb-e93d32a6b9a9.png)

# UML

![KakaoTalk_Photo_2022-12-25-22-56-43](https://user-images.githubusercontent.com/20445415/209470638-0910e7a7-4e70-4a2d-9785-289a431e6f2c.png)
![KakaoTalk_Photo_2022-12-25-22-56-47](https://user-images.githubusercontent.com/20445415/209470645-684f2160-de92-4abd-9b7a-ebc936438364.png)
![KakaoTalk_Photo_2022-12-25-16-52-30](https://user-images.githubusercontent.com/20445415/209460826-6179ab57-d72e-4b59-a465-aff9768bf82f.png)




# Getting Started

___

1. Clone the repo

  ```shell
    https://github.com/codestates/WBABEProject-04.git
  ```

2. Install Package

  ```shell
    go mod install
  ```

___

# API List
![image](https://user-images.githubusercontent.com/20445415/210963316-e85212a8-382b-494f-adc1-219e1063fc9b.png)
___

# 구현

## 메뉴 신규 등록 - 피주문자
### 요구사항

- **API |** 신규 메뉴 등록
  - 사업장에서 신규 메뉴 관련 정보를 등록하는 과정(ex. 메뉴 이름, 주문가능여부, 한정수량,  원산지, 가격, 맵기정도, etc)
  - 성공 여부를 리턴

### 구현

- URL : /menu
- Method : POST
- 입력 값 : JSON

  ```json
  {
      "name": "피자",
      "available": false,
      "quantity": 3,
      "favorites": false,
      "grade":4,
      "price":12000,
      "spiciness": 3
  }
  ```

- 출력 값 : JSON
  - 성공 시

      ```json
      {
        "result": "ok"
      }
      ```

  - 실패 시

      ```json
      {
        "Error": "Request Error",
        "body": "bnVsbA==",
        "error": [
            "already resistery menu",
            null
        ],
        "path": "/menu",
        "status": 422
      }
      ```

___

## 메뉴 수정 / 삭제 - 피주문자

### 요구사항

- **API |** 기존 메뉴 수정/삭제
  - 사업장에서 기존의 메뉴 정보 변경기능(ex. 가격변경, 원산지 변경, soldout)
  - 메뉴 삭제시, 실제 데이터 백업이나 뷰플래그를 이용한 안보임 처리
  - 금일 추천 메뉴 설정 변경, 리스트 출력
  - 성공 여부를 리턴

### 구현 - 기존 메뉴 수정

- URL : /menu/:menu
- Method : PUT
- 입력 값 : Parameter, JSON

  ```json
  {
    "price": 222200000,
    "soldout":true
  }
  ```

- 출력 값 : JSON
  - 성공 시

      ```json
      {
        "result": "ok"
      }
      ```

  - 실패 시
  
    ```json
    {
        "Error": "Request Error",
        "body": "bnVsbA==",
        "error": [
            "Menu is not registered.",
            {}
        ],
        "path": "/menu/:menu",
        "status": 422
    }
    ```

### 구현 - 기존 메뉴 삭제

- URL : /menu/:menu
- Method : DELETE
- 입력 값 : Parameter
- 성공 시

    ```json
    {
      "result": "ok"
    }
    ```

- 실패 시

    ```json
    {
        "Error": "Request Error",
        "body": "bnVsbA==",
        "error": [
            "It is not a registered menu",
            null
        ],
        "path": "/menu/:menu",
        "status": 400
    }
    ```

___

## 메뉴 리스트 출력 조회 - 주문자

### 요구사항

- **API |** 메뉴 리스트 조회 및 정렬(추천/평점/주문수/최신)
  - 각 카테고리별  sort 리스트 출력(ex. order by 추천, 평점, 재주문수, 최신)
  - 결과 5~10여개 임의 생성 출력, sorting 여부 확인

### 구현 - 추천 메뉴 조회

- URL : /order?con=favorites&ord=2
- Method : GET
- 입력 값 : Query
- 성공 시 : favorites 값이 true인 경우가 먼저 나타납니다.

    ```json
    {
        "data": [
            {
                "id": "63b6c72298dbd7d6d554e54a",
                "name": "삼겹살",
                "quantity": 3,
                "grade": 2,
                "origin": "국내산",
                "price": 12000,
                "spiciness": 4,
                "favorites": true,
                "count": 0,
                "createdat": "2023-01-05T12:48:34.727Z"
            },
            {
                "id": "63b6c72d98dbd7d6d554e54b",
                "name": "불고기",
                "quantity": 3,
                "grade": 5,
                "origin": "국내산",
                "price": 22000,
                "spiciness": 4,
                "favorites": true,
                "count": 0,
                "createdat": "2023-01-05T12:48:45.395Z"
            },
            {
                "id": "63b6c74198dbd7d6d554e54c",
                "name": "족발",
                "quantity": 3,
                "grade": 2,
                "origin": "국내산",
                "price": 32000,
                "spiciness": 1,
                "favorites": true,
                "count": 0,
                "createdat": "2023-01-05T12:49:05.291Z"
            },
            {
                "id": "63b6c77998dbd7d6d554e54e",
                "name": "묵사발",
                "quantity": 3,
                "grade": 4,
                "origin": "국내산",
                "price": 5100,
                "spiciness": 1,
                "favorites": true,
                "count": 0,
                "createdat": "2023-01-05T12:50:01.841Z"
            }
        ],
        "res": "ok"
    }
    ```

### 구현 - 주문순 조회

- URL : /order?con=count&ord=2
- Method : GET
- 입력 값 : Query
- 성공 시 : count 순으로 정렬되어 조회됩니다.

    ```json
    {
        "data": [
            {
                "id": "63b6c8db98dbd7d6d554e55e",
                "name": "전복죽",
                "quantity": 5,
                "grade": 3,
                "origin": "국내산",
                "price": 8000,
                "spiciness": 1,
                "favorites": true,
                "count": 5,
                "createdat": "2023-01-05T12:55:55.612Z"
            },
            {
                "id": "63b6c8e698dbd7d6d554e55f",
                "name": "소고기야채죽",
                "quantity": 5,
                "grade": 2,
                "origin": "국내산",
                "price": 8000,
                "spiciness": 1,
                "favorites": true,
                "count": 2,
                "createdat": "2023-01-05T12:56:06.345Z"
            },
            {
                "id": "63b6c8bc98dbd7d6d554e55c",
                "name": "부대찌개",
                "quantity": 5,
                "grade": 3,
                "origin": "국내산",
                "price": 8100,
                "spiciness": 1,
                "favorites": false,
                "count": 1,
                "createdat": "2023-01-05T12:55:24.768Z"
            },
            {
                "id": "63b6c88a98dbd7d6d554e559",
                "name": "김치찌개",
                "quantity": 5,
                "grade": 3,
                "origin": "국내산",
                "price": 9100,
                "spiciness": 2,
                "favorites": false,
                "count": 0,
                "createdat": "2023-01-05T12:54:34.649Z"
            }
        ],
        "res": "ok"
    }
    ```

### 구현 - 최신순 조회

- URL : /order?con=createdat&ord=2
- Method : GET
- 입력 값 : Query
- 성공 시 : 메뉴가 등록된 createdat순으로 정렬되어 조회됩니다.

    ```json
    {
        "data": [
            {
                "id": "63b6c90598dbd7d6d554e562",
                "name": "소고기",
                "quantity": 5,
                "grade": 5,
                "origin": "국내산",
                "price": 20000,
                "spiciness": 1,
                "favorites": false,
                "count": 0,
                "createdat": "2023-01-05T12:56:37.71Z"
            },
            {
                "id": "63b6c8f798dbd7d6d554e561",
                "name": "대창",
                "quantity": 5,
                "grade": 2,
                "origin": "국내산",
                "price": 9000,
                "spiciness": 1,
                "favorites": true,
                "count": 0,
                "createdat": "2023-01-05T12:56:23.386Z"
            },
            {
                "id": "63b6c8ee98dbd7d6d554e560",
                "name": "곱창",
                "quantity": 5,
                "grade": 3,
                "origin": "국내산",
                "price": 8000,
                "spiciness": 1,
                "favorites": true,
                "count": 2,
                "createdat": "2023-01-05T12:56:14.745Z"
            },
            {
                "id": "63b6c8e698dbd7d6d554e55f",
                "name": "소고기야채죽",
                "quantity": 5,
                "grade": 2,
                "origin": "국내산",
                "price": 8000,
                "spiciness": 1,
                "favorites": true,
                "count": 2,
                "createdat": "2023-01-05T12:56:06.345Z"
            }
        ],
        "res": "ok"
    }
    ```

### 구현 - 평점순 조회

- URL : /order?con=grade&ord=2
- Method : GET
- 입력 값 : Query
- 성공 시 : grade 순으로 정렬되어 조회됩니다.

    ```json
    {
        "data": [
            {
                "id": "63b6c90598dbd7d6d554e562",
                "name": "소고기",
                "quantity": 5,
                "grade": 5,
                "origin": "국내산",
                "price": 20000,
                "spiciness": 1,
                "favorites": false,
                "count": 0,
                "createdat": "2023-01-05T12:56:37.71Z"
            },
            {
                "id": "63b6c89898dbd7d6d554e55a",
                "name": "삼겹살",
                "quantity": 5,
                "grade": 4,
                "origin": "국내산",
                "price": 12100,
                "spiciness": 1,
                "favorites": true,
                "count": 0,
                "createdat": "2023-01-05T12:54:48.107Z"
            },
            {
                "id": "63b6c8db98dbd7d6d554e55e",
                "name": "전복죽",
                "quantity": 5,
                "grade": 3,
                "origin": "국내산",
                "price": 8000,
                "spiciness": 1,
                "favorites": true,
                "count": 5,
                "createdat": "2023-01-05T12:55:55.612Z"
            }
        ],
        "res": "ok"
    }
    ```

___

## 메뉴별 평점 및 리뷰 조회 - 주문자

### 요구사항

- **API |** 개별 메뉴별 평점 및 리뷰 보기
  - UI에서 메뉴 리스트에서 상기 리스트 출력에 따라 개별 메뉴를 선택했다고 가정
  - 해당 메뉴 선택시 메뉴에 따른 평점 및 리뷰 데이터 리턴

### 구현

- URL : /order/history/review/:menuID
- Method : GET
- 입력값 : Parameter
- 출력값 : JSON

    ```json
    {
        "data": [
            {
                "id": "63b6b1efb968de41b0688886",
                "content": "으엑",
                "menuid": "63b65a2cfc45a3f03a74bc9d",
                "customerid": "000000000000000000000000",
                "grade": 4,
                "iswrite": true,
                "createdat": "2023-01-05T11:18:07.863Z"
            },
            {
                "id": "63b6b254b968de41b0688887",
                "content": "으엑",
                "menuid": "63b65a2cfc45a3f03a74bc9d",
                "customerid": "63b672b0209b3e1230c7566a",
                "grade": 4,
                "iswrite": true,
                "createdat": "2023-01-05T11:19:48.01Z"
            },
            {
                "id": "63b78732f2721abf319572db",
                "content": "별로네요",
                "menuid": "63b65a2cfc45a3f03a74bc9d",
                "customerid": "63b672b0209b3e1230c7566a",
                "grade": 4,
                "iswrite": true,
                "createdat": "2023-01-06T02:28:02.525Z"
            },
            {
                "id": "63b78bb4f2721abf319572dd",
                "content": "맛있어요!!@#!@#",
                "menuid": "63b65a2cfc45a3f03a74bc9d",
                "customerid": "63b672b0209b3e1230c2266a",
                "grade": 4,
                "iswrite": true,
                "createdat": "2023-01-06T02:47:16.095Z"
            },
            {
                "id": "63b78bc3f2721abf319572de",
                "content": "재주문할게요!!#",
                "menuid": "63b65a2cfc45a3f03a74bc9d",
                "customerid": "63b672b0209b3e1230c2266a",
                "grade": 4,
                "iswrite": true,
                "createdat": "2023-01-06T02:47:31.657Z"
            }
        ],
        "res": "ok"
    }
    ```

___

## 메뉴별 평점 작성 - 주문자

### 요구사항

- **API |** 과거 주문 내역 중, 평점 및 리뷰 작성
  - 해당 주문내역을 기준, 평점 정보, 리뷰 스트링을 입력받아 과거 주문내역 업데이트 저장
  - 성공 여부 리턴

### 구현

- URL : order/history/review/:orderID
- Method : POST
- 입력 값 : JSON

    ```json
    {
        "content" : "별로네요",
        "menuid" : "63b65a2cfc45a3f03a74bc9d",
        "grade":4,
        "customerid": "63b672b0209b3e1230c7566a"
    }
    ```

- 출력 값 : JSON

    ```json
    {
        "res": "ok"
    }
    ```

___

## 주문 - 주문자

### 요구사항

- **API |** UI에서 메뉴 리스트에서 해당 메뉴 선택, 주문 요청 및 초기상태 저장
  - 주문정보를 입력받아 주문 저장(ex. 선택 메뉴 정보, 전화번호, 주소등 정보를 입력받아 DB 저장)
  - 주문 내역 초기상태 저장
  - 금일 주문 받은 일련번호-주문번호 리턴

### 구현

- URL: /order
- Method : POST
- 입력 값 : JSON

    ```json
    {
        "nicname":"김동규",
        "phone":"01012341234",
        "address":"서울시 이곳저곳",
        "orders": [
            {
                "menus" :[
                    {
                        "name": "전복죽",
                        "spiciness":3
                    }
                ]
            },
               {
                "menus" :[
                    {
                        "name": "곱창"
                    }
                ]
            }
        ]
    }
    ```

- 출력 값 : JSON

    ```json
    {
        "orderNumber": [
            "63b7795fcf081264cc7dd24e"
        ],
        "res": "ok"
    }
    ```

___

## 주문 변경 - 주문자

### 요구사항

- **API |** 메뉴 변경 및 추가
  - 메뉴 추가시 상태조회 후 `배달중`일 경우 실패 알림
    - 성공 실패 알림, 실패시 신규주문으로 전환
  - 메뉴 변경시 상태가 `조리중`, `배달중`일 경우 확인
    - 성공 실패 알림

### 구현 - 메뉴 추가 (정상 추가 가능)

- URL : /order/:orderID
- Method : POST
- 입력 값 : Parameter, JSON

    ```json
    {
        "customerid": "63b7795fcf081264cc7dd24c",
        "menus" :
        [
            {
                "name": "된장찌개"
            }
        ]
    }
    ```

- 출력 값

    ```json
    {
        "Data": "63b77f27cf081264cc7dd24f",
        "contents": "The menu has been added normally.",
        "res": "ok",
        "status": "add order"
    }
    ```

### 구현 - 메뉴 추가 시 배달 중 일 경우(신규 주문으로 전환)

- URL : /order/:orderID
- Method : POST
- 입력 값 : Parameter, JSON

    ```json
    {
        "customerid": "63b7795fcf081264cc7dd24c",
        "menus" :
        [
            {
                "name": "된장찌개"
            }
        ]
    }
    ```

- 출력 값

    ```json
    {
        "Data": "63b78655f2721abf319572da",
        "contents": "Adding a menu failed, requesting a new order.",
        "res": "ok",
        "status": "new order"
    }
    ```

### 구현 - 메뉴 변경 시 상태가 조리중 배달 중 일경우

- URL : /order/:orderID
- Method : PUT
- 입력값 : Parameter, JSON

  ```json
  {
    "menus" :[
        {
            "name": "김치찌개",
            "spiciness":8
        }
    ]
  }
  ```

- 출력값 : JSON
  - 성공 시(조리중이거나 배달중이 아닐떄)

      ```json
      {
          "Data": {
              "id": "63b7ad0c662b7b69d4302ea1",
              "customerid": "000000000000000000000000",
              "menus": [
                  {
                      "id": "63b6c88a98dbd7d6d554e559",
                      "name": "김치찌개",
                      "quantity": 5,
                      "grade": 3,
                      "origin": "국내산",
                      "price": 9100,
                      "spiciness": 2,
                      "favorites": false,
                      "count": 2,
                      "createdat": "2023-01-05T12:54:34.649Z"
                  }
              ],
              "status": 0,
              "createdAt": "2023-01-06T05:03:44.513Z"
          },
          "contents": "The menu has changed..",
          "res": "ok",
          "status": "changed order"
      }
      ```

  - 실패 시(조리중이거나 배달중일 때)

      ```json
      {
          "Error": "Request Error",
          "body": "bnVsbA==",
          "error": [
              "The Order cannot be changed.",
              null
          ],
          "path": "/order/:ordernumber",
          "status": 400
      }
      ```

## 주문 내역 조회 - 주문자

### 요구사항

- **API |** 주문내역 조회
  - 현재 주문내역 리스트 및 상태 조회 - 하기 **주문 상태 조회**에서도 사용
    - ex. 접수중/조리중/배달중 etc
    - 없으면 null 리턴
  - 과거 주문내역 리스트 최신순으로 출력
    - 없으면 null 리턴

### 구현 - 현재 주문내역 리스트 가져오기(배달완료가 아직 안된 목록)

- URL: /order/:customerID
- Method : GET
- 입력값 : Parameter
- 출력값

  ```json
    {
      "data": 
      [
        {
          "id": "63b7795fcf081264cc7dd24e",
          "customerid": "63b7795fcf081264cc7dd24c",
          "menus": [
            {
              "id": "63b6c8db98dbd7d6d554e55e",
              "name": "전복죽",
              "quantity": 5,
              "grade": 3,
              "origin": "국내산",
              "price": 8000,
              "spiciness": 1,
              "favorites": true,
              "count": 5,
              "createdat": "2023-01-05T12:55:55.612Z"
            },
            {
              "id": "63b6c8ee98dbd7d6d554e560",
              "name": "곱창",
              "quantity": 5,
              "grade": 3,
              "origin": "국내산",
              "price": 8000,
              "spiciness": 1,
              "favorites": true,
              "count": 2,
              "createdat": "2023-01-05T12:56:14.745Z"
            }
          ],
          "status": 3,
          "createdAt": "2023-01-06T01:29:03.396Z"
        }
      ],
      "res": "ok"
    }
  ```

### 구현 - 과거 주문내역 리스트 가져오기(status code: 7 배달완료된 목록)

- URL : /order/history/:customerID
- Method : GET
- 입력값 : Parameter
- 출력값

    ```json
    {
      "data": [
        {
          "id": "63b7795fcf081264cc7dd24e",
          "customerid": "63b7795fcf081264cc7dd24c",
          "menus": [
            {
              "id": "63b6c8db98dbd7d6d554e55e",
              "name": "전복죽",
              "quantity": 5,
              "grade": 3,
              "origin": "국내산",
              "price": 8000,
              "spiciness": 1,
              "favorites": true,
              "count": 5,
              "createdat": "2023-01-05T12:55:55.612Z"
            },
            {
              "id": "63b6c8ee98dbd7d6d554e560",
              "name": "곱창",
              "quantity": 5,
              "grade": 3,
              "origin": "국내산",
              "price": 8000,
              "spiciness": 1,
              "favorites": true,
              "count": 2,
              "createdat": "2023-01-05T12:56:14.745Z"
            }
          ],
          "status": 7,
          "createdAt": "2023-01-06T01:29:03.396Z"
        }
      ],
      "res": "ok"
    }
    ```

## 주문 상태 조회 - 피주문자

### 요구사항

- **API |** 현재 주문내역 리스트 조회
- **API |** 각 메뉴별 상태 변경
  - ex. 상태 : 접수중/접수취소/추가접수/접수-조리중/배달중/배달완료 등을 이용 상태 저장
  - 각 단계별 사업장에서 상태 업데이트
    - **접수중 → 접수** or **접수취소 → 조리중** or **추가주문 → 배달중**
    - 성공여부 리턴

### 구현 - 현재 주문내역 리스트 조회(주문접수가 완료된 것)

- URL : /menu/order
- Method : GET
- 출력 값

    ```json
    {
      "data": [
        {
          "id": "63b6c05ebb7deaac6525c751",
          "customerid": "63b6c05ebb7deaac6525c74f",
          "menus": [
            {
              "id": "63b65a2cfc45a3f03a74bc9e",
              "name": "고구마",
              "soldout": true,
              "quantity": 3,
              "grade": 3,
              "origin": "국내산",
              "price": 100000,
              "spiciness": 3,
              "favorites": false,
              "count": 1,
              "createdat": "2023-01-05T05:03:40.616Z"
            },
            {
              "id": "63b673c7787b1370a54ebc7d",
              "name": "감자",
              "quantity": 3,
              "grade": 4,
              "origin": "국내산",
              "price": 12000,
              "spiciness": 3,
              "favorites": false,
              "count": 1,
              "createdat": "2023-01-05T06:52:55.146Z"
            }
          ],
          "status": 3,
          "createdAt": "2023-01-05T12:19:42.173Z"
        },
        {
          "id": "63b6c05ebb7deaac6525c754",
          "customerid": "63b6c05ebb7deaac6525c752",
          "menus": [
            {
              "id": "63b65a2cfc45a3f03a74bc9e",
              "name": "고구마",
              "soldout": true,
              "quantity": 3,
              "grade": 3,
              "origin": "국내산",
              "price": 100000,
              "spiciness": 3,
              "favorites": false,
              "count": 1,
              "createdat": "2023-01-05T05:03:40.616Z"
            },
            {
              "id": "63b673c7787b1370a54ebc7d",
              "name": "감자",
              "quantity": 3,
              "grade": 4,
              "origin": "국내산",
              "price": 12000,
              "spiciness": 3,
              "favorites": false,
              "count": 1,
              "createdat": "2023-01-05T06:52:55.146Z"
            }
          ],
          "status": 3,
          "createdAt": "2023-01-05T12:19:42.773Z"
        },
      ],
      "result": "ok"
    }
    ```

### 구현 - 각 메뉴별 상태 변경

- URL : /menu/order
- Method : PUT
- 입력 값 : JSON

  ```json
  {
    "orderid": "63b7795fcf081264cc7dd24e",
    "status":7
  }
  ```

- 출력 값 : JSON
  - 성공 시

      ```json
      {
          "result": "ok"
      }
      ```

  - 실패 시

      ```json
      {
          "Error": "Request Error",
          "body": "bnVsbA==",
          "error": [
              "fail, Please enter your json correctly",
              null
          ],
          "path": "/menu/order",
          "status": 400
      }
      ```

___

## Contact

___

- Email: [abnormal5626@gmail.com]()
- Project Link: [프로젝트 링크](https://github.com/codestates/WBABEProject-04)
  
