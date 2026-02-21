# dart_fss 라이브러리 다운로드
!pip install dart_fss

# dart_fss 라이브러리 실행 및 재무제표 저장
import dart_fss as dart

# Open DART API KEY 설정
dart.set_api_key(api_key='6a5cb2029b267e54613ca3a2244a15cd3af26807')

# DART 에 공시된 회사 리스트 불러오기
corp_list = dart.get_corp_list()

# LG에너지솔루션 검색
lg_energy = corp_list.find_by_corp_name('LG에너지솔루션', exactly=True)[0]

# 2020년부터 연간 연결재무제표 불러오기
fs = lg_energy.extract_fs(bgn_de='20200101')

# 재무제표 검색 결과를 엑셀파일로 저장 ( 기본저장위치: 실행폴더/fsdata )
fs.save()

