# JobPlanet Web Crawling

기업 데이터(평점, 리뷰, 통계 등)를 자동으로 수집하는 Python Selenium 기반 크롤러입니다.

## 📦 프로젝트 구성

- `Crawling_Jobplanet.py` : 크롤러 메인 코드 (Selenium + BeautifulSoup)
- `enterprise_df_14_utf8_data.csv` : 크롤링 대상 기업명 목록(csv)
- `jobplanet_crawling_progress.csv` : 진행상황 중간 저장(자동 생성)
- `jobplanet_crawling_error.csv` : 에러 기업/사유 기록(자동 생성)
- `README.md` : 프로젝트 설명 파일

## 🚀 주요 기능

- JobPlanet에서 기업명 자동 검색 및 상세 페이지 이동
- 평점, 세부 통계 등 자동 수집
- 기업별 중복 처리, 중간저장/복구, 에러로그 저장
- tqdm 진행상황 표시(터미널)
- headless(창 없는) 크롬으로 빠르고 조용하게 수집

## 💻 사용 방법

1. **필수 라이브러리 설치**

    ```bash
    pip install selenium pandas beautifulsoup4 tqdm
    ```

    - *크롬 브라우저*와 *chromedriver* 설치 필요  
      (chromedriver 버전은 [여기](https://chromedriver.chromium.org/downloads)에서 본인 크롬에 맞게 설치)

2. **기업명 목록 준비**
    - `enterprise_df_14_utf8_data.csv` 파일에 `기업명` 컬럼이 포함되어 있어야 합니다.

3. **크롤링 실행**

    ```bash
    python Crawling_Jobplanet.py
    ```

4. **진행상황/에러**
    - `jobplanet_crawling_progress.csv`: 수집된 데이터(중간저장)
    - `jobplanet_crawling_error.csv`: 크롤링 실패(검색결과 없음, 기타 예외 등)

5. **결과 확인**
    - 결과 CSV 파일에서 원하는 기업의 평점/통계/리뷰수 등을 확인할 수 있습니다.

## 📝 코드 주요 옵션

- **크롤링 대상 기업 개수**  
  코드 내에서 `target_companies_name = pd.DataFrame(..., columns=["기업명"])` 부분의 개수 조절로 테스트/전체 선택 가능.
- **진행상황 자동 저장 주기**: 10개 기업마다 자동 저장
- **실패 기업 로그 기록**: 에러 원인까지 저장

## ⚠️ 참고/주의사항

- 크롤링 도중 강제 종료되어도 기존 진행상황에서 이어서 실행 가능
- JobPlanet 사이트 구조 변경 시 CSS selector도 함께 수정 필요
- 반복 실행 시, 사이트에서 자동화(봇) 차단이 걸릴 수 있으니 1~2초 sleep을 유지 권장
