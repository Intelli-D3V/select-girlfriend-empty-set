# 실습
Real MySQL을 학습하면서 진행할 실습 내용들을 정리

## 환경 구성
- docker container 생성 및 실행
```bash
docker compose up -d
```

- DB 접속 정보
    - Host: localhost
    - Port: 3306
    - User: user
    - Password: password
    - Database: studydb

## 기본 Table
기본 테스트를 위해 생성해 둔 깡통 Table이다.

### ERD
```mermaid
erDiagram
    CUSTOMERS {
      INT customer_id PK
      VARCHAR name
      VARCHAR email "UNIQUE"
      DATETIME created_at
    }
    PRODUCTS {
      INT product_id PK
      VARCHAR name
      TEXT description
      DECIMAL price
      INT stock
      DATETIME created_at
    }
    ORDERS {
      INT order_id PK
      INT customer_id FK
      DATETIME order_date
      ENUM status "('pending','completed','cancelled')"
    }
    ORDER_ITEMS {
      INT order_item_id PK
      INT order_id FK
      INT product_id FK
      INT quantity
      DECIMAL unit_price
    }

    CUSTOMERS ||--o{ ORDERS : "places"
    ORDERS ||--o{ ORDER_ITEMS : "contains"
    PRODUCTS ||--o{ ORDER_ITEMS : "referenced in"
```

## 기타
- init.sql 수정 시 반영을 위해서는 volume 삭제해줘야 한다.