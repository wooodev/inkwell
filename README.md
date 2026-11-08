# inkwell

회원이 글을 쓰고 댓글로 소통하는 블로그·커뮤니티 API 서비스.

## 기술 스택

- Python 3.12, Django 5.2, Django REST Framework
- PostgreSQL 16 (Docker Compose)
- uv (의존성 관리), pytest-django, ruff

## 실행 방법

### 준비

- [uv](https://docs.astral.sh/uv/)
- Docker (Docker Compose 포함)

### 1. 의존성 설치

```bash
uv sync
```

`.python-version`에 맞는 Python 3.12 가상환경(`.venv`)이 만들어진다.

### 2. 환경변수 파일 만들기

```bash
cp .env.example .env
```

로컬에서 5432 포트를 이미 쓰고 있다면 `.env`의 `POSTGRES_PORT`를 다른 값(예: 5433)으로 바꾼다.

### 3. PostgreSQL 실행

```bash
docker compose up -d --wait
```

### 4. 마이그레이션과 개발 서버

```bash
uv run --env-file .env python manage.py migrate
uv run --env-file .env python manage.py runserver
```

`--env-file .env`를 붙여야 Django가 `.env`의 DB 접속 정보를 읽는다.

## 테스트와 코드 검사

```bash
uv run --env-file .env pytest
uv run ruff check .
uv run ruff format --check .
```
