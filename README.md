### Day1: GitHub & 환경 설정 (2025-09-19)
- **Homebrew 설치**
  - macOS 패키지 매니저(Homebrew) 설치
  - `echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile`
  - 터미널 시작 시 자동으로 Homebrew 환경 변수를 불러오도록 설정

- **GitHub 연동**
  - `git clone https://github.com/<GitHub아이디>/rna-seq-bootcamp.git`
  - Personal Access Token(PAT) 생성 및 입력
  - GitHub 원격 저장소와 로컬 폴더 연동 성공 확인

- **폴더 구조 확인**
  - `data/.gitkeep`, `results/.gitkeep` 파일 확인 → 빈 폴더라도 Git에 반영
  - `README.md` 생성 및 기본 기록 시작

- **배운 점 정리**
  - Homebrew는 macOS에서 소프트웨어를 관리하는 도구
  - GitHub 연동 시 HTTPS+토큰 방식 사용
  - `.gitkeep`은 빈 폴더를 Git에 포함시키기 위한 관습적인 파일

---

### Day2: FASTQ 기초 다루기 (2025-09-22)
- **폴더 이동**
  - `pwd`, `cd ~/rna-seq-bootcamp`, `cd data`, `cd ..`, `cd ~`
  - 현재 작업 위치 확인 및 폴더 이동 방법 익힘

- **파일 다운로드**
  - `curl -L -o sample.fastq https://raw.githubusercontent.com/hbctraining/Intro-to-rnaseq-hpc-O2/master/data/sample.fastq`
  - FASTQ 예제 파일 다운로드

- **파일 미리보기**
  - `head -20 sample.fastq` → 앞 20줄 확인
  - `less sample.fastq` → 스크롤로 확인

- **파일 검색/라인 수 세기**
  - `grep "Day1" README.md` → 특정 문자열 찾기
  - `grep -i "day1" README.md` → 대소문자 구분 없이 검색
  - `grep -n "Day1" README.md` → 줄 번호 출력
  - `wc -l sample.fastq` → 총 35줄 확인
  - `grep -c "^@" sample.fastq` → read 개수 = 9개 확인

- **FASTQ 구조 확인**
  - FASTQ는 4줄 단위 구조:  
    1. `@` → read ID  
    2. 시퀀스 (A/T/G/C)  
    3. `+` 기호  
    4. 품질(quality) 정보
  - `awk 'NR % 4 == 0' sample.fastq` → 품질 줄만 출력

- **배운 점 정리**
  - FASTQ는 read별 4줄 구조로 이루어져 있음
  - `head`, `less`, `grep`, `wc`, `awk` 등을 활용해 데이터 구조를 빠르게 점검 가능
  - macOS 기본 `sed`는 `~` 문법을 지원하지 않음 → `awk`로 대체

---

### Day3: Conda 환경 & Jupyter Notebook (2025-09-25)
- **Conda 설치**
  - Miniconda 설치 완료, `conda --version`으로 확인
  - `conda create -n rna-seq python=3.11` → 가상환경 생성
  - `conda activate rna-seq` → 가상환경 활성화

- **Jupyter Notebook 실행**
  - `which python` → 가상환경에 설치된 Python 확인
  - `jupyter notebook` 실행 후 브라우저에서 접속
  - `day3.ipynb` 생성 및 테스트 코드 실행

- **데이터 처리 연습**
  - pandas, matplotlib 설치
  - 작은 CSV(`sample.csv`) 불러오기 → `pd.read_csv("sample.csv")`
  - 요약 통계 `df.describe()`, 단순 bar plot 작성

- **GitHub 기록**
  - `git add`, `git commit -m "Day3: README와 sample.csv 업로드"`, `git push origin main`
  - GitHub에 day3.ipynb, sample.csv 반영

- **배운 점 정리**
  - Conda: 가상환경 관리 툴, 각 프로젝트마다 독립된 환경 구성 가능
  - Jupyter Notebook: 브라우저 기반 인터랙티브 실행 환경
  - Git 워크플로우: add → commit → push 순서로 원격 저장소에 반영

---

### Day4: Pandas 데이터 처리 심화 (2025-09-29)
- **데이터 불러오기 & 탐색**
  - `df = pd.read_csv("data/sample.csv")`
  - `df.head()`, `df.describe()`로 데이터 구조 확인

- **데이터 정렬 & 필터링**
  - `df.sort_values(by="expression", ascending=False)` → 내림차순 정렬
  - `df[df["expression"] > 7]` → 조건 필터링
  - `df.query("expression == 10.5 or expression == 8.2")` → SQL 스타일 필터링

- **새로운 컬럼 추가**
  - Z-score 계산:
    ```python
    df["z"] = (df["expression"] - df["expression"].mean()) / df["expression"].std()
    ```

- **데이터 저장 & 재활용**
  - `df.to_csv("data/day4_result.csv", index=False)` → 결과 저장
  - 저장 시 `index=False`는 인덱스를 저장하지 않도록 설정

- **시각화**
  - `plt.scatter(df["expression"], df["z"])` → scatter plot
  - `plt.xlabel`, `plt.ylabel`, `plt.title` 로 그래프 꾸미기

- **GitHub 기록**
  - `README.md`에 Day4 내용 추가
  - `git add README.md notebooks/day4.ipynb notebooks/day4_result.csv`
  - `git commit -m "Day4: z-score 계산 및 시각화"`
  - `git push origin main`

- **배운 점 정리**
  - pandas로 정렬, 필터링, 새로운 컬럼 생성 가능
  - Z-score 계산으로 데이터 표준화 연습
  - matplotlib으로 기본적인 시각화 수행
  - GitHub에 정리된 기록과 결과물 업로드하는 루틴 확립
