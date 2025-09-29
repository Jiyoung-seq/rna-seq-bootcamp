# RNA-seq Bootcamp

This repository records my 12-week RNA-seq analysis training.

## Progress
- Day1: Environment setup (Homebrew, Git)
- Folders created: data/, scripts/, results/, notebooks/

### Day2: FASTQ 기초 다루기 (2025-09-22)  
- **폴더 이동**  
  - `pwd`, `cd ~/rna-seq-bootcamp`, `cd data`, `cd ..`, `cd ~`  
  - 현재 작업 위치 확인 및 폴더 이동 방법 익힘.  

- **파일 다운로드**  
  - `curl -L -o sample.fastq https://raw.githubusercontent.com/hbctraining/Intro-to-rnaseq-hpc-O2/master/data/sample.fastq`  
  - FASTQ 예제 파일 다운로드.  

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
  - FASTQ는 read별 4줄 구조로 이루어져 있음.  
  - `head`, `less`, `grep`, `wc`, `awk` 등을 활용해 데이터 구조를 빠르게 점검 가능.  
  - macOS 기본 `sed`는 `~` 문법을 지원하지 않음 → `awk`로 대체.  

### Day3
- conda 환경에서 Jupyter Notebook 실행

- pandas를 이용한 DataFrame 생성 및 요약 통계

- matplotlib으로 barplot, boxplot, histogram 시각화

- CSV 파일 저장 및 불러오기 실습


## Day4 
- pandas로 z-score 계산 

- 데이터프레임 저장 (to_csv) 

- matplotlib을 이용한 scatter plot 시각화
