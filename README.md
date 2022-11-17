# The-system-for-LIS-patients
-------------------------------------
✏✔💫

LIS(Locked-in syndrome)✏



# 모듈구성✏
- FindBlink.py: 눈 깜빡임을 검출
- analysis.py:  파일을 읽고 눈 깜빡임을 검출한 뒤 검출했다면 그에 맞는 결과 반환 
- App.py : flask 실행
- Preprocessing.py : 전처리 과정 (노이즈 제거, band-pass filter, FFT)
- Hz_potential.py : 해당 구간과 주파수의 평균 전위 값
- Index_cal.py : time 문자열을 시간으로 변환 및 time 비교하여 index 반환
- Load_data.py : mave 데이터 를 실시간으로 읽어 옴
- Ssvep.py : ssvep 주파수 데이터 분석을 실행한 뒤 보고 있는 주파수 반환

# 모듈 별 설명✏

## FinfBlink ✔

눈 깜박임으로 인한 뇌파데이터의 노이즈를 이용하여 눈깜박임을 검출합니다.
5초 사이에 눈 깜박임이 다수 검출된다면 사용자가 서비스 시작을 위한 의도적 행동이라 판단합니다.

1) raw_data에서 최근 5초 동안의 index를 가져옵니다.
2) find_peak 함수를 사용하여 피크를 검출합니다. 눈 깜박임으로 인한 노이즈를 상대적으로 강하기 때문에 height, distance 파라미터를 반복적 실험 후 적절히 조정하였습니다.
3) peak의 개수가 7개 이상이면 마지막 피크의 index위치를 반환합니다.

![Untitled](https://user-images.githubusercontent.com/74172467/202417392-d509f677-dbc3-4ba4-a62a-82192633f4ce.png)
### 그외 시도해본 방법
+ 눈 깜박임으로 인한 Delta, Theata변화량을 사용하는 것보다 raw_data의 노이즈를 활용하는 것이 효과적이었습니다.
+ 한쪽 눈만 감는 경우를 시도해보았지만 유의미한 차이를 확인할 수 없었습니다.

## analysis ✔
눈 깜박임 검출 뒤 서비스가 시작되면 10초 정도의 여유 이후 분석할 csv파일을 읽어옵니다.

## App ✔
flask를 실행합니다.
서버와 함수들을 연결해주는 역할을 합니다.

## preprocessing ✔
뇌파의 전처리에 필요한 함수들을 담아놨습니다.
- ICA 독립성분 분석
- FFT 

## Hz_potential ✔
