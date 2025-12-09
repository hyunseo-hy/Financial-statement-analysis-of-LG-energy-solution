# 엑셀 파일 불러오기 및 확인
import pandas as pd
file_path = '/content/fsdata/01515323_annual.xlsx'
df = pd.read_excel(file_path)
print(df.head())

# 비율분석
import pandas as pd
FS = "01515323_annual.xlsx"
bs_df = pd.read_excel(FS, sheet_name = "Data_bs")
is_df = pd.read_excel(FS, sheet_name = "Data_is")
cf_df = pd.read_excel(FS, sheet_name = "Data_cf")

y_is = "20240101-20241231"  # 손익계산서 상 2023-2024 column
y24  = "20241231"           # 재무상태표 당기 (2024 기말 시점)
y23  = "20231231"           # 재무상태표 전기 (2023 기말 시점)

def get(df, name, col):
    row = df[df.iloc[:,2].astype(str).str.contains(name, na=False)]
    return float(row[col].iloc[0])


#비율분석에 필요한 값들 추출 (손익계산서)
rev  = get(is_df, "매출액", y_is)
cogs = get(is_df, "매출원가", y_is)
gp   = get(is_df, "매출총이익", y_is)
op   = get(is_df, "영업이익", y_is)
ni   = get(is_df, "지배기업의 소유주지분", y_is) # 당기 순이익(소유주지분)

#비율분석에 필요한 값들 추출 (재무상태표)
ta24, ta23 = get(bs_df, "자산총계", y24), get(bs_df, "자산총계", y23) #총자산
eq24, eq23 = get(bs_df, "지배기업의 소유주지분", y24), get(bs_df, "지배기업의 소유주지분", y23) #지배기업 자기자본
curA24, curA23 = get(bs_df, "유동자산", y24), get(bs_df, "유동자산", y23) #유동자산
curL24, curL23 = get(bs_df, "유동부채", y24), get(bs_df, "유동부채", y23) #유동부채
ar24, ar23   = get(bs_df, "매출채권", y24), get(bs_df, "매출채권", y23) #매출채권
inv24, inv23 = get(bs_df, "재고자산", y24), get(bs_df, "재고자산", y23) #재고자산
ap24, ap23   = get(bs_df, "매입채무", y24), get(bs_df, "매입채무", y23) #매입채무
pp24, pp23   = get(bs_df, "유형자산", y24), get(bs_df, "유형자산", y23) #유형자산

#  분석을 위한 부채 및 차입금 항목
TL24, TL23  = get(bs_df, "부채총계", y24) , get(bs_df, "부채총계", y23) #총부채
SD24, SD23  = get(bs_df, "유동성차입금", y24) , get(bs_df, "유동성차입금", y23) #유동성차입금
LD24, LD23 = get(bs_df, "비유동성차입금", y24), get(bs_df, "비유동성차입금", y23) #비유동성차입금
NCA24, NCA23 = get(bs_df, "비유동자산", y24), get(bs_df, "비유동자산", y23) #비유동자산
NCL24, NCL23 = get(bs_df, "비유동부채", y24), get(bs_df, "비유동부채", y23) #비유동부채

# 현금흐름표
# 이자보상배율 계산용, 현금유출(-)로 표기되므로 abs()로 절대값 처리
int_paid = abs(get(cf_df, "이자의 지급", y_is))

# 재무상태표 수치 평균화작업
avg_eq  = (eq24 + eq23) / 2          # 평균 자기자본
avg_ta  = (ta24 + ta23) / 2          # 평균 총자산
avg_wc  = ((curA24-curL24) + (curA23-curL23)) / 2 # 평균 순운전자본 (유동자산-유동부채)
avg_ar  = (ar24 + ar23) / 2          # 평균 매출채권
avg_inv = (inv24 + inv23) / 2        # 평균 재고자산
avg_ap  = (ap24 + ap23) / 2          # 평균 매입채무
avg_pp  = (pp24 + pp23) / 2          # 평균 유형자산
avg_curA = (curA24 + curA23) / 2     # 평균 유동자산
avg_curL = (curL24 + curL23) / 2     # 평균 유동부채

# 추가 평균화 작업
avg_TL  = (TL24 + TL23) / 2          # 평균 부채총계
avg_SD  = (SD24 + SD23) / 2          # 평균 유동성차입금
avg_LD  = (LD24 + LD23) / 2          # 평균 비유동성차입금
avg_NCA = (NCA24 + NCA23) / 2        # 평균 비유동자산
avg_NCL = (NCL24 + NCL23) / 2        # 평균 비유동부채

#비율계산
results = {
    "ROE(지배기업)%": ni / avg_eq * 100,
    "총자산순영업이익률%": op / avg_ta * 100,

    "매출총이익률%": gp / rev * 100,
    "매출액영업이익률%": op / rev * 100,
    "매출액순이익률%": ni / rev * 100,

    "영업운전자본회전율(회)": rev / avg_wc,
    "매출채권회전율(회)": rev / avg_ar,
    "재고자산회전율(회)": cogs / avg_inv,
    "매입채무회전율(회)": cogs / avg_ap,
    "유형자산회전율(회)": rev / avg_pp,

    "유동비율%": avg_curA / avg_curL * 100,
    "당좌비율%": (avg_curA - avg_inv) / avg_curL * 100,

    "부채비율%": avg_TL / avg_eq * 100,
    "차입부채비율%": (avg_SD + avg_LD) / avg_eq * 100,
    "이자보상비율(배)": op / int_paid,
    "고정장기적합률%": avg_NCA / (avg_eq + avg_NCL) * 100
}

#엑셀 다운로드
results_df = pd.DataFrame(results.items(), columns=["ratio","value"])
print(results_df)
results_df.to_excel("ratio_results.xlsx", index=False)
from google.colab import files
files.download("ratio_results.xlsx")