# 🏫 Smart Campus API (v0.3.0)

FastAPI 기반 **스마트 캠퍼스 강의실 관리 데모 API**입니다.
(빈 강의실 조회, 일정 확인, 예약 기능 포함)

---

## 🚀 실행 방법 (Windows)

```bat
py -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
python -m uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

> 실행 후 브라우저에서 **[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)** 로 접속하면 Swagger UI에서 API를 직접 테스트할 수 있습니다.

---

## 📦 주요 엔드포인트

| Method | Path                        | 설명                     |
| :----: | :-------------------------- | :--------------------- |
|   GET  | `/buildings`                | 건물 코드 및 층 정보 조회        |
|   GET  | `/rooms`                    | 강의실 목록 (필터 가능)         |
|   GET  | `/rooms/free-now`           | 현재 빈 강의실 목록 (수업+예약 반영) |
|   GET  | `/rooms/{room_id}/timeline` | 하루 단위 점유/빈 시간대 조회      |
|  POST  | `/rooms/reserve`            | 강의실 예약 생성              |

---

## 🧠 예시 요청

### 🔹 지금 빈 강의실 조회

```bash
curl "http://127.0.0.1:8000/rooms/free-now?building=ENG&min_capacity=30"
```

### 🔹 타임라인 조회

```bash
curl "http://127.0.0.1:8000/rooms/1/timeline?date=2025-11-10"
```

### 🔹 예약 생성

```bash
curl -X POST "http://127.0.0.1:8000/rooms/reserve" ^
  -H "Content-Type: application/json" ^
  -d "{\"room_id\":1,\"date\":\"2025-11-10\",\"start\":\"15:00\",\"end\":\"16:00\",\"user\":\"정다은\"}"
```

---

## 🧩 기술 스택

* **Python 3.11+**
* **FastAPI / Uvicorn** (백엔드 프레임워크)
* **Pydantic** (데이터 검증)
* **CORS 허용**: React 개발서버(`localhost:3000`)에서 바로 호출 가능

---

## 🧱 프로젝트 구조

```
smart-campus-api/
 ├─ main.py              # FastAPI 서버 메인 파일
 ├─ requirements.txt     # 패키지 의존성
 ├─ README.md            # 실행/사용법 문서
 └─ .venv/               # 가상환경 (로컬 전용)
```

---

## 🗺️ 향후 확장 아이디어

* DB 연동 (SQLite → PostgreSQL)
* 사용자 인증 및 권한 구분 (학생/관리자)
* 예약 취소·변경 API
* 예약/이용 통계 시각화
* 학사 달력, 공휴일 반영

---

## 🤝 협업 가이드

* **main 브랜치**: 안정 버전 유지
* **feature/** 브랜치: 기능 단위 작업 (예: `feature/reservation-db`)
* **PR**: Swagger 캡처나 응답 예시 포함해 리뷰 요청

---

## 📄 라이선스

MIT License
