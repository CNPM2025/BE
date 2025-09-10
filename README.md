# Architecture

```bash
 ├── migrations/                     # alembic migration scripts
│   └── versions/                   # migration history
│
├── scripts/
│   └── run_postgres.sh             # script docker-compose hoặc psql để start DB
│
├── src/
│   ├── api/
│   │   ├── controllers/
│   │   │   ├── user_controller.py
│   │   │   ├── todo_controller.py
│   │   │   ├── lessonplan_controller.py
│   │   │   ├── test_controller.py
│   │   │   ├── question_controller.py
│   │   │   ├── answersheet_controller.py
│   │   │   └── result_controller.py
│   │   │
│   │   ├── schemas/
│   │   │   ├── user.py
│   │   │   ├── todo.py
│   │   │   ├── lessonplan.py
│   │   │   ├── test.py
│   │   │   ├── question.py
│   │   │   ├── answersheet.py
│   │   │   └── result.py
│   │   │
│   │   ├── middleware.py           # logging, auth
│   │   ├── responses.py            # chuẩn hóa response
│   │   └── requests.py             # helper validate request
│   │
│   ├── infrastructure/
│   │   ├── services/
│   │   │   ├── email_service.py    # ví dụ: gửi mail
│   │   │   └── ocr_service.py      # OCR grading service
│   │   │
│   │   ├── databases/
│   │   │   ├── base.py             # Base = declarative_base()
│   │   │   ├── mssql.py            # engine, session, init
│   │   │   └── postgres.py         # nếu bạn support Postgres
│   │   │
│   │   ├── repositories/
│   │   │   ├── user_repository.py
│   │   │   ├── todo_repository.py
│   │   │   ├── lessonplan_repository.py
│   │   │   ├── test_repository.py
│   │   │   ├── question_repository.py
│   │   │   ├── answersheet_repository.py
│   │   │   └── result_repository.py
│   │   │
│   │   └── models/
│   │       ├── user_model.py
│   │       ├── todo_model.py
│   │       ├── lessonplan_model.py
│   │       ├── test_model.py
│   │       ├── question_model.py
│   │       ├── answersheet_model.py
│   │       └── result_model.py
│   │
│   ├── domain/
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   ├── models/
│   │   │   ├── user.py
│   │   │   ├── todo.py
│   │   │   ├── lessonplan.py
│   │   │   ├── test.py
│   │   │   ├── question.py
│   │   │   ├── answersheet.py
│   │   │   └── result.py
│   │   └── interfaces/
│   │       ├── iuser_repository.py
│   │       ├── itodo_repository.py
│   │       ├── ilessonplan_repository.py
│   │       ├── itest_repository.py
│   │       ├── iquestion_repository.py
│   │       ├── ianswersheet_repository.py
│   │       └── iresult_repository.py
│   │
│   ├── services/
│   │   ├── user_service.py
│   │   ├── todo_service.py
│   │   ├── lessonplan_service.py
│   │   ├── test_service.py
│   │   ├── question_service.py
│   │   ├── answersheet_service.py
│   │   └── result_service.py
│   │
│   ├── app.py
│   ├── config.py
│   ├── cors.py
│   ├── create_app.py
│   ├── dependency_container.py
│   ├── error_handler.py
│   └── logging.py
│
├── requirements.txt
└── README.md
```

## Domain Layer

## Services Layer

## Infrastructure Layer

## Download source code (CMD)
    git clone https://github.com/ChienNguyensrdn/Flask-CleanArchitecture.git
## Kiểm tra đã cài python đã cài đặt trên máy chưa
    python --version
## Run app

 - Bước 1: Tạo môi trường ảo co Python (phiên bản 3.x)
     ## Windows:
     		py -m venv .venv
     ## Unix/MacOS:
     		python3 -m venv .venv
   - Bước 2: Kích hoạt môi trường:
     ## Windows:
     		.venv\Scripts\activate.ps1
     ### Nếu xảy ra lỗi active .venv trên winos run powshell -->Administrator
         Set-ExecutionPolicy RemoteSigned -Force
     ## Unix/MacOS:
     		source .venv/bin/activate
     
   - Bước 3: Cài đặt các thư viện cần thiết
     ## Install:
     		pip install -r requirements.txt
   - Bước 4: Chạy mã xử lý dữ liệu
     ## Run:
    		python app.py


     Truy câp http://localhost:6868/docs



## Create file .env in folder /src/.env
    
    # Flask settings
    FLASK_ENV=development
    SECRET_KEY=your_secret_key
    
    # SQL Server settings
    DB_USER=sa
    DB_PASSWORD=Aa@123456
    DB_HOST=127.0.0.1
    DB_PORT=1433
    DB_NAME=FlaskApiDB
    
    
    DATABASE_URI = "mssql+pymssql://sa:Aa%40123456@127.0.0.1:1433/FlaskApiDB"

## pull image MS SQL server 
    
    ```bash
    docker pull mcr.microsoft.com/mssql/server:2025-latest
    ```
## Install MS SQL server in docker 
    ```bash
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=Aa123456" -p 1433:1433 --name sql1 --hostname sql1 -d  mcr.microsoft.com/mssql/server:2025-latest
    ```
## Test connect SQL server 

## ORM Flask (from sqlalchemy.orm )
Object Relational Mapping

Ánh xạ 1 class (OOP)  model src/infrastructure/models --> Table in database 
Ánh xạ các mối quan hệ (Relational) -- Khoá ngoại CSDL 
(n-n): many to many 
