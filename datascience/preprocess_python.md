# データサイエンス100本ノック（構造化データ加工編） - Python

### P-001

レシート明細のデータフレーム（df_receipt）から全項目の先頭10件を表示し、どのようなデータを保有しているか目視で確認せよ。

```python
df_receipt.head(10)
```

### P-002

レシート明細のデータフレーム（df_receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、10件表示させよ。

```python
df_receipt.head(10)[['sales_ymd', 'customer_id', 'product_cd', 'amount']]
```

### P-003

レシート明細のデータフレーム（df_receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、10件表示させよ。ただし、sales_ymdはsales_dateに項目名を変更しながら抽出すること。

```python
df_p003 = df_receipt.head(10)[['sales_ymd', 'customer_id', 'product_cd', 'amount']]
df_p003.rename(columns={'sales_ymd': 'sales_date'})
```

### P-004

レシート明細のデータフレーム（df_receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

```python
df_receipt[df_receipt.customer_id == 'CS018205000001'][['sales_ymd', 'customer_id', 'product_cd', 'amount']]
```

### P-005

レシート明細のデータフレーム（df_receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"
* 売上金額（amount）が1,000以上

```python
df_p005 = df_receipt[(df_receipt.customer_id == 'CS018205000001') & (df_receipt.amount >= 1000)]
df_p005[['sales_ymd', 'customer_id', 'product_cd', 'amount']]
```

### P-006

レシート明細データフレーム「df_receipt」から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上数量（quantity）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"
* 売上金額（amount）が1,000以上または売上数量（quantity）が5以上

```python
df_p006 = df_receipt[(df_receipt.customer_id == 'CS018205000001') & ((df_receipt.amount >= 1000) | (df_receipt.quantity >= 5))]
df_p006[['sales_ymd', 'customer_id', 'product_cd', 'quantity', 'amount']]
```

### P-007

レシート明細のデータフレーム（df_receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"
* 売上金額（amount）が1,000以上2,000以下

```python
df_p007 = df_receipt[(df_receipt.customer_id == 'CS018205000001') & (1000 <= df_receipt.amount) & (df_receipt.amount <= 2000)]
df_p007[['sales_ymd', 'customer_id', 'product_cd', 'amount']]
```

### P-008

レシート明細のデータフレーム（df_receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"
* 商品コード（product_cd）が"P071401019"以外

```python
df_p007 = df_receipt[(df_receipt.customer_id == 'CS018205000001') & (df_receipt.product_cd != 'P071401019')]
df_p007[['sales_ymd', 'customer_id', 'product_cd', 'amount']]
```

### P-009

以下の処理において、出力結果を変えずにORをANDに書き換えよ。  
`df_store.query('not(prefecture_cd == "13" | floor_area > 900)')`

```python
df_store.query('prefecture_cd != "13" & floor_area <= 900')
```

### P-010

店舗データフレーム（df_store）から、店舗コード（store_cd）が"S14"で始まるものだけ全項目抽出し、10件だけ表示せよ。

```python
df_store.query('store_cd.str.startswith("S14")', engine='python')
```

### P-011

顧客データフレーム（df_customer）から顧客ID（customer_id）の末尾が1のものだけ全項目抽出し、10件だけ表示せよ。

```python
df_customer.query('customer_id.str.endswith("1")', engine='python')
```

### P-012

店舗データフレーム（df_store）から横浜市の店舗だけ全項目表示せよ。

```python
df_store.query('address.str.contains("横浜市")', engine='python')
```

### P-013

顧客データフレーム（df_customer）から、ステータスコード（status_cd）の先頭がアルファベットのA〜Fで始まるデータを全項目抽出し、10件だけ表示せよ。

```python
df_customer.query('status_cd.str.match("^[A-F].*$")', engine='python')
```

### P-014

顧客データフレーム（df_customer）から、ステータスコード（status_cd）の末尾が数字の1〜9で終わるデータを全項目抽出し、10件だけ表示せよ。

```python
df_customer.query('status_cd.str.match("^.*[1-9]$")', engine='python')
```

### P-015

顧客データフレーム（df_customer）から、ステータスコード（status_cd）の先頭がアルファベットのA〜Fで始まり、末尾が数字の1〜9で終わるデータを全項目抽出し、10件だけ表示せよ。

```python
df_customer.query('status_cd.str.match("^[A-F].*[1-9]$")', engine='python')
```

### P-016

店舗データフレーム（df_store）から、電話番号（tel_no）が3桁-3桁-4桁のデータを全項目表示せよ。

```python
df_store.query('tel_no.str.match("^\d{3}-\d{3}-\d{4}$")', engine='python')
```

### P-017

顧客データフレーム（df_customer）を生年月日（birth_day）で高齢順にソートし、先頭10件を全項目表示せよ。

```python
df_customer.sort_values('birth_day').head(10)
```

### P-018

顧客データフレーム（df_customer）を生年月日（birth_day）で若い順にソートし、先頭10件を全項目表示せよ。

```python
df_customer.sort_values('birth_day', ascending=False).head(10)
```

### P-019

レシート明細データフレーム（df_receipt）に対し、1件あたりの売上金額（amount）が高い順にランクを付与し、先頭10件を抽出せよ。項目は顧客ID（customer_id）、売上金額（amount）、付与したランクを表示させること。なお、売上金額（amount）が等しい場合は同一順位を付与するものとする。

```python
df_p19 = df_receipt.sort_values('amount', ascending=False).head(10)[['customer_id', 'amount']]
df_p19['rank'] = df_p19.rank(ascending=False, method='min').amount.astype(int)
df_p19
```

### P-020

レシート明細データフレーム（df_receipt）に対し、1件あたりの売上金額（amount）が高い順にランクを付与し、先頭10件を抽出せよ。項目は顧客ID（customer_id）、売上金額（amount）、付与したランクを表示させること。なお、売上金額（amount）が等しい場合でも別順位を付与すること。

```python
df_p20 = df_receipt.sort_values('amount', ascending=False).head(10)[['customer_id', 'amount']]
df_p20['rank'] = df_p20.rank(ascending=False, method='first').amount.astype(int)
df_p20
```

### P-021

レシート明細データフレーム（df_receipt）に対し、件数をカウントせよ。

```python
len(df_receipt)
```

### P-022

レシート明細データフレーム（df_receipt）の顧客ID（customer_id）に対し、ユニーク件数をカウントせよ。

```python
len(df_receipt['customer_id'].unique())
```

### P-023

レシート明細データフレーム（df_receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）と売上数量（quantity）を合計せよ。

```python
df_receipt[['store_cd', 'amount', 'quantity']].groupby('store_cd').sum()
```

### P-024

レシート明細データフレーム（df_receipt）に対し、顧客ID（customer_id）ごとに最も新しい売上日（sales_ymd）を求め、10件表示せよ。

```python
df_receipt[['customer_id', 'sales_ymd']].groupby('customer_id').max().head(10)
```

### P-025

レシート明細データフレーム（df_receipt）に対し、顧客ID（customer_id）ごとに最も古い売上日（sales_ymd）を求め、10件表示せよ。

```python
df_receipt[['customer_id', 'sales_ymd']].groupby('customer_id').min().head(10)
```

### P-026

レシート明細データフレーム（df_receipt）に対し、顧客ID（customer_id）ごとに最も新しい売上日（sales_ymd）と古い売上日を求め、両者が異なるデータを10件表示せよ。

```python
df_026 = df_receipt[['customer_id', 'sales_ymd']].groupby('customer_id').agg(['min', 'max'])
df_026[df_026[('sales_ymd', 'min')] != df_026[('sales_ymd', 'max')]]
```

### P-027

レシート明細データフレーム（df_receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の平均を計算し、降順でTOP5を表示せよ。

```python
df_receipt[['store_cd', 'amount']].groupby('store_cd').mean().sort_values('amount', ascending=False).head(5)
```

### P-028

レシート明細データフレーム（df_receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の中央値を計算し、降順でTOP5を表示せよ。

```python
df_receipt[['store_cd', 'amount']].groupby('store_cd').median().sort_values('amount', ascending=False).head(5)
```

### P-029

レシート明細データフレーム（df_receipt）に対し、店舗コード（store_cd）ごとに商品コード（product_cd）の最頻値を求めよ。

```python
df_receipt[['store_cd', 'product_cd', 'receipt_no']].groupby(['store_cd', 'product_cd']) \
  .count().reset_index().groupby('store_cd').max()
```

### P-030

レシート明細データフレーム（df_receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の標本分散を計算し、降順でTOP5を表示せよ。

```python
df_receipt[['store_cd', 'amount']].groupby('store_cd').var().sort_values('amount', ascending=False).head(5)
```

### P-031

レシート明細データフレーム（df_receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の標本標準偏差を計算し、降順でTOP5を表示せよ。

```python
df_receipt[['store_cd', 'amount']].groupby('store_cd').std().sort_values('amount', ascending=False).head(5)
```

### P-032

レシート明細データフレーム（df_receipt）の売上金額（amount）について、25％刻みでパーセンタイル値を求めよ。

```python
df_receipt.amount.quantile([0.0, 0.25, 0.50, 0.75, 1.00])
```

### P-033

レシート明細データフレーム（df_receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の平均を計算し、330以上のものを抽出せよ。

```python
df_receipt[['store_cd', 'amount']].groupby('store_cd').mean().query('amount >= 330')
```

### P-034

レシート明細データフレーム（df_receipt）に対し、顧客ID（customer_id）ごとに売上金額（amount）を合計して全顧客の平均を求めよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。

```python
df_receipt[['customer_id', 'amount']].groupby('customer_id').sum() \
  .query('not customer_id.str.startswith("Z")', engine='python').mean()
```

### P-035

レシート明細データフレーム（df_receipt）に対し、顧客ID（customer_id）ごとに売上金額（amount）を合計して全顧客の平均を求め、平均以上に買い物をしている顧客を抽出せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。なお、データは10件だけ表示させれば良い。

```python
amount_by_customer = df_receipt.query('not customer_id.str.startswith("Z")', engine='python')[['customer_id', 'amount']].groupby('customer_id').sum()
amount_by_customer[amount_by_customer.amount >= amount_by_customer.amount.mean()]
```

### P-036

レシート明細データフレーム（df_receipt）と店舗データフレーム（df_store）を内部結合し、レシート明細データフレームの全項目と店舗データフレームの店舗名（store_name）を10件表示させよ。

```python
df_receipt.merge(df_store[['store_cd', 'store_name']], on='store_cd', how='inner').head(10)
```

### P-037

商品データフレーム（df_product）とカテゴリデータフレーム（df_category）を内部結合し、商品データフレームの全項目とカテゴリデータフレームの小区分名（category_small_name）を10件表示させよ。

```python
df_product.merge(
    df_category[['category_major_cd', 'category_medium_cd', 'category_small_cd', 'category_small_name']],
    on=['category_major_cd', 'category_medium_cd', 'category_small_cd'],
    how='inner'
).head(10)
```

### P-038

顧客データフレーム（df_customer）とレシート明細データフレーム（df_receipt）から、各顧客ごとの売上金額合計を求めよ。ただし、売上実績がない顧客については売上金額を0として表示させること。また、顧客は性別コード（gender_cd）が女性（1）であるものを対象とし、非会員（顧客IDが"Z"から始まるもの）は除外すること。なお、結果は10件だけ表示させれば良い。

```python
target_customers = df_customer.query('gender_cd == "1" and not customer_id.str.startswith("Z")', engine='python')
amounts = df_receipt[['customer_id', 'amount']].groupby('customer_id').sum()
target_customers.merge(amounts, on='customer_id', how='left').fillna(0).head(10)
```

### P-039

レシート明細データフレーム（df_receipt）から売上日数の多い顧客の上位20件と、売上金額合計の多い顧客の上位20件を抽出し、完全外部結合せよ。ただし、非会員（顧客IDが"Z"から始まるもの）は除外すること。

```python
df = df_receipt.query('not customer_id.str.startswith("Z")', engine='python')
top_freq_customers = df.groupby('customer_id').nunique('sales_ymd').sort_values('sales_ymd').tail(20)
top_sales_customers = df[['customer_id', 'amount']].groupby('customer_id').sum().sort_values('amount').tail(20)
pd.concat((top_freq_customers.reset_index().customer_id, top_sales_customers.reset_index().customer_id))
```

### P-040

全ての店舗と全ての商品を組み合わせると何件のデータとなるか調査したい。店舗（df_store）と商品（df_product）を直積した件数を計算せよ。

```python
len(df_store) * len(df_product)
```

### P-041

レシート明細データフレーム（df_receipt）の売上金額（amount）を日付（sales_ymd）ごとに集計し、前日からの売上金額増減を計算せよ。なお、計算結果は10件表示すればよい。

```python
df_receipt[['sales_ymd', 'amount']].groupby('sales_ymd').sum().sort_index().diff().head(10)
```

### P-042

レシート明細データフレーム（df_receipt）の売上金額（amount）を日付（sales_ymd）ごとに集計し、各日付のデータに対し、１日前、２日前、３日前のデータを結合せよ。結果は10件表示すればよい。

```python
daily_sales = df_receipt[['sales_ymd', 'amount']].groupby('sales_ymd').sum().sort_index()
for d in range(1, 4):
    daily_sales[f'amount_{d}d_ago'] = daily_sales.shift(d).amount
daily_sales.head(10)
```

### P-043

レシート明細データフレーム（df_receipt）と顧客データフレーム（df_customer）を結合し、性別（gender）と年代（ageから計算）ごとに売上金額（amount）を合計した売上サマリデータフレーム（df_sales_summary）を作成せよ。性別は0が男性、1が女性、9が不明を表すものとする。  
ただし、項目構成は年代、女性の売上金額、男性の売上金額、性別不明の売上金額の4項目とすること（縦に年代、横に性別のクロス集計）。また、年代は10歳ごとの階級とすること。

```python
df = df_receipt[['customer_id', 'amount']].merge(df_customer[['customer_id', 'gender', 'age']], on='customer_id', how='left')
df.gender.fillna('不明', inplace=True)
df['age_range'] = df.age.apply(lambda x: '不明' if np.isnan(x) else f'{int(x//10*10)}歳代')
df_sales_summary = pd.pivot_table(data=df, index='age_range', columns='gender', values='amount', aggfunc='sum')
df_sales_summary
```

### P-044

前設問で作成した売上サマリデータフレーム（df_sales_summary）は性別の売上を横持ちさせたものであった。このデータフレームから性別を縦持ちさせ、年代、性別コード、売上金額の3項目に変換せよ。ただし、性別コードは男性を"00"、女性を"01"、不明を"99"とする。

```python
gender_cd = {'男性': '00', '女性': '01', '不明': '99'}
gender_dfs = [] 
for col in df_sales_summary:
    gender_df = df_sales_summary[[col]].rename(columns={col: 'amount'})
    gender_df['gender_cd'] = gender_cd[col]
    gender_dfs.append(gender_df)
pd.concat(gender_dfs)
```

### P-045

顧客データフレーム（df_customer）の生年月日（birth_day）は日付型でデータを保有している。これをYYYYMMDD形式の文字列に変換し、顧客ID（customer_id）とともに抽出せよ。データは10件を抽出すれば良い。

```python
df = df_customer[['customer_id', 'birth_day']]
pd.concat((df['customer_id'], df['birth_day'].apply(lambda x: x.strftime('%Y%m%d'))), axis=1).head(10)
```

### P-046

顧客データフレーム（df_customer）の申し込み日（application_date）はYYYYMMDD形式の文字列型でデータを保有している。これを日付型に変換し、顧客ID（customer_id）とともに抽出せよ。データは10件を抽出すれば良い。

```python
pd.concat((df_customer['customer_id'], df_customer['application_date'].apply(lambda x: datetime.strptime(x, '%Y%m%d'))), axis=1).head(10)
```

### P-047

レシート明細データフレーム（df_receipt）の売上日（sales_ymd）はYYYYMMDD形式の数値型でデータを保有している。これを日付型に変換し、レシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。データは10件を抽出すれば良い。

```python
pd.concat((
    df_receipt[['receipt_no', 'receipt_sub_no']],
    df_receipt.sales_ymd.apply(lambda x: datetime.strptime(str(x), '%Y%m%d')),
), axis=1).head(10)
```

### P-048

レシート明細データフレーム（df_receipt）の売上エポック秒（sales_epoch）は数値型のUNIX秒でデータを保有している。これを日付型に変換し、レシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。データは10件を抽出すれば良い。

```python
pd.concat((
    df_receipt[['receipt_no', 'receipt_sub_no']],
    df_receipt.sales_epoch.apply(lambda x: datetime.fromtimestamp(x)),
), axis=1).head(10)
```

### P-049

レシート明細データフレーム（df_receipt）の売上エポック秒（sales_epoch）を日付型に変換し、「年」だけ取り出してレシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。データは10件を抽出すれば良い。

```python
pd.concat((
    df_receipt[['receipt_no', 'receipt_sub_no']],
    df_receipt.sales_epoch.apply(lambda x: datetime.fromtimestamp(x).year),
), axis=1).head(10)
```

### P-050

レシート明細データフレーム（df_receipt）の売上エポック秒（sales_epoch）を日付型に変換し、「月」だけ取り出してレシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。なお、「月」は0埋め2桁で取り出すこと。データは10件を抽出すれば良い。

```python
pd.concat((
    df_receipt[['receipt_no', 'receipt_sub_no']],
    df_receipt.sales_epoch.apply(lambda x: datetime.fromtimestamp(x).strftime('%m')),
), axis=1).head(10)
```

### P-051

レシート明細データフレーム（df_receipt）の売上エポック秒を日付型に変換し、「日」だけ取り出してレシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。なお、「日」は0埋め2桁で取り出すこと。データは10件を抽出すれば良い。

```python
pd.concat((
    df_receipt[['receipt_no', 'receipt_sub_no']],
    df_receipt.sales_epoch.apply(lambda x: datetime.fromtimestamp(x).strftime('%d')),
), axis=1).head(10)
```

### P-052

シート明細データフレーム（df_receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計の上、売上金額合計に対して2,000円以下を0、2,000円より大きい金額を1に2値化し、顧客ID、売上金額合計とともに10件表示せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。

```python
df =df_receipt[['customer_id', 'amount']].query('not customer_id.str.startswith("Z")', engine='python').groupby('customer_id').sum()
df['good_sale_customer'] = df.amount.apply(lambda x: int(x > 2000))
df.head(10)
```

### P-053

顧客データフレーム（df_customer）の郵便番号（postal_cd）に対し、東京（先頭3桁が100〜209のもの）を1、それ以外のものを0に２値化せよ。さらにレシート明細データフレーム（df_receipt）と結合し、全期間において売上実績がある顧客数を、作成した2値ごとにカウントせよ。

```python
df_tokyo_customer = pd.concat((
    df_customer.customer_id,
    df_customer.postal_cd.apply(lambda x: int(100 <= int(x.split('-')[0]) <= 209))
), axis=1).rename(columns={'postal_cd': 'is_tokyo'})
df_receipt[['customer_id']].merge(df_tokyo_customer, on='customer_id', how='left') \
  .groupby('is_tokyo').nunique('customer_id')
```

### P-054

顧客データフレーム（df_customer）の住所（address）は、埼玉県、千葉県、東京都、神奈川県のいずれかとなっている。都道府県毎にコード値を作成し、顧客ID、住所とともに抽出せよ。値は埼玉県を11、千葉県を12、東京都を13、神奈川県を14とすること。結果は10件表示させれば良い。

```python
pref_cds = {'埼玉県': 11, '千葉県': 12, '東京都': 13, '神奈川県': 14}
def get_pref_cds(address, default=0):
    for pref, cd in pref_cds.items():
        if address.startswith(pref):
            return cd
    return default
df = df_customer[['customer_id', 'address']].copy()
df['pref_cd'] = df.address.apply(get_pref_cds)
df.head(10)
```

### P-055

レシート明細データフレーム（df_receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、その合計金額の四分位点を求めよ。その上で、顧客ごとの売上金額合計に対して以下の基準でカテゴリ値を作成し、顧客ID、売上金額合計とともに表示せよ。カテゴリ値は上から順に1〜4とする。結果は10件表示させれば良い。

* 最小値以上第一四分位未満
* 第一四分位以上第二四分位未満
* 第二四分位以上第三四分位未満
* 第三四分位以上

```python
sales_by_customer = df_receipt[['customer_id', 'amount']].groupby('customer_id').sum()
ths = sales_by_customer.amount.quantile([0.25, 0.5, 0.75])
def get_customer_category(amount):
    for i, th in enumerate(ths):
        if amount < th:
            return i + 1
    return len(ths) + 1
sales_by_customer['customer_category'] = sales_by_customer.amount.apply(get_customer_category)
sales_by_customer.head(10)
```

### P-056

顧客データフレーム（df_customer）の年齢（age）をもとに10歳刻みで年代を算出し、顧客ID（customer_id）、生年月日（birth_day）とともに抽出せよ。ただし、60歳以上は全て60歳代とすること。年代を表すカテゴリ名は任意とする。先頭10件を表示させればよい。

```python
def get_age_range(age):
    age_range = int(age // 10 * 10) if age < 60 else 60
    return f'{age_range}歳代'
df = df_customer[['customer_id', 'birth_day']].copy()
df['age_range'] = df_customer.age.apply(get_age_range)
df.head(10)
```

### P-057

前問題の抽出結果と性別（gender）を組み合わせ、新たに性別×年代の組み合わせを表すカテゴリデータを作成せよ。組み合わせを表すカテゴリの値は任意とする。先頭10件を表示させればよい。

```python
df['category'] = df_customer['gender'] + '_' + df['age_range']
df.head(10)
```

### P-058

顧客データフレーム（df_customer）の性別コード（gender_cd）をダミー変数化し、顧客ID（customer_id）とともに抽出せよ。結果は10件表示させれば良い。

```python
pd.concat((
    df_customer.customer_id, 
    pd.get_dummies(df_customer[['gender_cd']])
), axis=1).head(10)
```

### P-059

レシート明細データフレーム（df_receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、売上金額合計を平均0、標準偏差1に標準化して顧客ID、売上金額合計とともに表示せよ。標準化に使用する標準偏差は、不偏標準偏差と標本標準偏差のどちらでも良いものとする。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。結果は10件表示させれば良い。

```python
df = df_receipt.query('not customer_id.str.startswith("Z")', engine='python')[['customer_id', 'amount']].groupby('customer_id').sum()
df['amount_normalized'] = (df.amount - df.amount.mean()) / df.amount.std()
df.head(10)
```

### P-060

レシート明細データフレーム（df_receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、売上金額合計を最小値0、最大値1に正規化して顧客ID、売上金額合計とともに表示せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。結果は10件表示させれば良い。

```python
df = df_receipt.query('not customer_id.str.startswith("Z")', engine='python')[['customer_id', 'amount']].groupby('customer_id').sum()
df['amount_normalized'] = (df['amount'] - df['amount'].min()) / (df['amount'].max() - df['amount'].min())
df.head(10)
```

### P-061

レシート明細データフレーム（df_receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、売上金額合計を常用対数化（底=10）して顧客ID、売上金額合計とともに表示せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。結果は10件表示させれば良い。

```python
df = df_receipt.query('not customer_id.str.startswith("Z")', engine='python')[['customer_id', 'amount']].groupby('customer_id').sum()
df['amount_log'] = np.log10(df['amount'])
df.head(10)
```

### P-062

レシート明細データフレーム（df_receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、売上金額合計を自然対数化(底=e）して顧客ID、売上金額合計とともに表示せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。結果は10件表示させれば良い。

```python
df = df_receipt.query('not customer_id.str.startswith("Z")', engine='python')[['customer_id', 'amount']].groupby('customer_id').sum()
df['amount_log'] = np.log10(df['amount'])
df.head(10)
```

### P-063

商品データフレーム（df_product）の単価（unit_price）と原価（unit_cost）から、各商品の利益額を算出せよ。結果は10件表示させれば良い。

```python
pd.concat((
    df_product[['product_cd']],
    df_product.unit_price - df_product.unit_cost
), axis=1).head(10)
```

### P-064

商品データフレーム（df_product）の単価（unit_price）と原価（unit_cost）から、各商品の利益率の全体平均を算出せよ。 ただし、単価と原価にはNULLが存在することに注意せよ。

```python
df = df_product.copy().query('not (unit_price.isnull() or unit_cost.isnull())', engine='python')
((df.unit_price - df.unit_cost) / df.unit_price).mean()
```

### P-065

商品データフレーム（df_product）の各商品について、利益率が30%となる新たな単価を求めよ。ただし、1円未満は切り捨てること。そして結果を10件表示させ、利益率がおよそ30％付近であることを確認せよ。ただし、単価（unit_price）と原価（unit_cost）にはNULLが存在することに注意せよ。

```python
df = df_product.copy()
df['new_price'] = np.floor(df['unit_cost'] / 0.7)
df['profit_ratio'] = (df['new_price'] - df['unit_cost']) / df['new_price']
df.head(10)
```

### P-066

商品データフレーム（df_product）の各商品について、利益率が30%となる新たな単価を求めよ。今回は、1円未満を丸めること（四捨五入または偶数への丸めで良い）。そして結果を10件表示させ、利益率がおよそ30％付近であることを確認せよ。ただし、単価（unit_price）と原価（unit_cost）にはNULLが存在することに注意せよ

```python
df = df_product.copy()
df['new_price'] = np.floor(df['unit_cost'] / 0.7)
df['profit_ratio'] = (df['new_price'] - df['unit_cost']) / df['new_price']
df.head(10)
```

### P-067

商品データフレーム（df_product）の各商品について、利益率が30%となる新たな単価を求めよ。今回は、1円未満を切り上げること。そして結果を10件表示させ、利益率がおよそ30％付近であることを確認せよ。ただし、単価（unit_price）と原価（unit_cost）にはNULLが存在することに注意せよ。

```python
df = df_product.copy()
df['new_price'] = np.ceil(df['unit_cost'] / 0.7)
df['profit_ratio'] = (df['new_price'] - df['unit_cost']) / df['new_price']
df.head(10)
```

### P-068

商品データフレーム（df_product）の各商品について、消費税率10%の税込み金額を求めよ。 1円未満の端数は切り捨てとし、結果は10件表示すれば良い。ただし、単価（unit_price）にはNULLが存在することに注意せよ。

```python
df = df_product.copy()
df['tax_include_price'] = np.floor(df['unit_cost'] * 1.1)
df.head(10)
```

### P-069

レシート明細データフレーム（df_receipt）と商品データフレーム（df_product）を結合し、顧客毎に全商品の売上金額合計と、カテゴリ大区分（category_major_cd）が"07"（瓶詰缶詰）の売上金額合計を計算の上、両者の比率を求めよ。抽出対象はカテゴリ大区分"07"（瓶詰缶詰）の売上実績がある顧客のみとし、結果は10件表示させればよい。

```python
df = df_receipt[['customer_id', 'product_cd', 'amount']].merge(
    df_product[['product_cd', 'category_major_cd']],
    on='product_cd',
    how='inner'
)
df1 = df.groupby('customer_id').sum()
df1.rename(columns={'amount': 'total_sales'}, inplace=True)
df2 = df.query('category_major_cd == "07"').groupby('customer_id').sum()
df2.rename(columns={'amount': 'category07_sales'}, inplace=True)
df3 = df1.join(df2, how='inner')
df3['category07_ratio'] = df3['category07_sales'] / df3['total_sales']
df3.head(10)
```

### P-070

レシート明細データフレーム（df_receipt）の売上日（sales_ymd）に対し、顧客データフレーム（df_customer）の会員申込日（application_date）からの経過日数を計算し、顧客ID（customer_id）、売上日、会員申込日とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値、application_dateは文字列でデータを保持している点に注意）。

```python
df1 = df_customer[['customer_id', 'application_date']].copy()
df1['application_date_dt'] = df1['application_date'].apply(lambda x: datetime.strptime(x, '%Y%m%d'))
df2 = df_receipt[['customer_id', 'sales_ymd']].copy()
df2['sales_dt'] = df2['sales_ymd'].apply(lambda x: datetime.strptime(str(x), '%Y%m%d'))
df = df2.merge(df1, on='customer_id')
df['passed_dt'] = df['sales_dt'] - df['application_date_dt']
df.head(10)[['customer_id', 'sales_ymd', 'application_date', 'passed_dt']]
```

### P-071

レシート明細データフレーム（df_receipt）の売上日（sales_ymd）に対し、顧客データフレーム（df_customer）の会員申込日（application_date）からの経過月数を計算し、顧客ID（customer_id）、売上日、会員申込日とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値、application_dateは文字列でデータを保持している点に注意）。1ヶ月未満は切り捨てること。

```
df1 = df_customer[['customer_id', 'application_date']].copy()
df1['application_date_dt'] = df1['application_date'].apply(lambda x: datetime.strptime(x, '%Y%m%d'))
df2 = df_receipt[['customer_id', 'sales_ymd']].copy()
df2['sales_dt'] = df2['sales_ymd'].apply(lambda x: datetime.strptime(str(x), '%Y%m%d'))
df = df2.merge(df1, on='customer_id')
df['passed_m'] = df.apply(lambda row: row['sales_dt'].year * 12 + row['sales_dt'].month - row['application_date_dt'].year * 12 - row['application_date_dt'].month, axis=1)
df.head(10)[['customer_id', 'sales_ymd', 'application_date', 'passed_m']]
```

### P-072

レシート明細データフレーム（df_receipt）の売上日（sales_ymd）に対し、顧客データフレーム（df_customer）の会員申込日（application_date）からの経過年数を計算し、顧客ID（customer_id）、売上日、会員申込日とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値、application_dateは文字列でデータを保持している点に注意）。1年未満は切り捨てること。

```python
df1 = df_customer[['customer_id', 'application_date']].copy()
df1['application_date_dt'] = df1['application_date'].apply(lambda x: datetime.strptime(x, '%Y%m%d'))
df2 = df_receipt[['customer_id', 'sales_ymd']].copy()
df2['sales_dt'] = df2['sales_ymd'].apply(lambda x: datetime.strptime(str(x), '%Y%m%d'))
df = df2.merge(df1, on='customer_id')
df['passed_y'] = df.apply(lambda row: row['sales_dt'].year - row['application_date_dt'].year, axis=1)
df.head(10)[['customer_id', 'sales_ymd', 'application_date', 'passed_y']]
```

### P-073

レシート明細データフレーム（df_receipt）の売上日（sales_ymd）に対し、顧客データフレーム（df_customer）の会員申込日（application_date）からのエポック秒による経過時間を計算し、顧客ID（customer_id）、売上日、会員申込日とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値、application_dateは文字列でデータを保持している点に注意）。なお、時間情報は保有していないため各日付は0時0分0秒を表すものとする

```python
df1 = df_customer[['customer_id', 'application_date']].copy()
df1['application_date_dt'] = df1['application_date'].apply(lambda x: datetime.strptime(x, '%Y%m%d'))
df2 = df_receipt[['customer_id', 'sales_ymd']].copy()
df2['sales_dt'] = df2['sales_ymd'].apply(lambda x: datetime.strptime(str(x), '%Y%m%d'))
df = df2.merge(df1, on='customer_id')
df['passed_epoch'] = (df['sales_dt'] - df['application_date_dt']).apply(lambda x: x.total_seconds())
df.head(10)[['customer_id', 'sales_ymd', 'application_date', 'passed_epoch']]
```

### P-074

レシート明細データフレーム（df_receipt）の売上日（sales_ymd）に対し、当該週の月曜日からの経過日数を計算し、売上日、当該週の月曜日付とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値でデータを保持している点に注意）。

```python
from datetime import timedelta
df = df_receipt[['sales_ymd']].copy()
df['sales_ymd'] = df['sales_ymd'].apply(lambda x: datetime.strptime(str(x), '%Y%m%d'))
df['elapsed_since_monday'] = df['sales_ymd'].apply(lambda x: x.isoweekday() - 1)
df['monday'] = df['sales_ymd'].apply(lambda x: x - timedelta(days=x.isoweekday() - 1))
df.head(10)
```

### P-075

顧客データフレーム（df_customer）からランダムに1%のデータを抽出し、先頭から10件データを抽出せよ。

```python
df_customer.sample(frac=0.01).head(10)
```

### P-076

顧客データフレーム（df_customer）から性別（gender_cd）の割合に基づきランダムに10%のデータを層化抽出し、性別ごとに件数を集計せよ。

```python
for gender in df_customer.gender_cd.unique():
    df_gender = df_customer.query(f'gender_cd == "{gender}"')
    print(f'gender: {gender}, num of 10% sample: {len(df_gender.sample(frac=0.1))}')
```

### P-077

レシート明細データフレーム（df_receipt）の売上金額（amount）を顧客単位に合計し、合計した売上金額の外れ値を抽出せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。なお、ここでは外れ値を平均から3σ以上離れたものとする。結果は10件表示させれば良い。

```python
df = df_receipt.query('not customer_id.str.startswith("Z")', engine='python')[['customer_id', 'amount']].groupby('customer_id').sum()
amount_mean = df.mean()['amount']
amount_std = df.std()['amount']
outliers = df.query(f'amount < {amount_mean - amount_std * 3} or {amount_mean + amount_std * 3} < amount')
outliers.head(10)
```

### P-078

レシート明細データフレーム（df_receipt）の売上金額（amount）を顧客単位に合計し、合計した売上金額の外れ値を抽出せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。なお、ここでは外れ値を第一四分位と第三四分位の差であるIQRを用いて、「第一四分位数-1.5×IQR」よりも下回るもの、または「第三四分位数+1.5×IQR」を超えるものとする。結果は10件表示させれば良い。

```python
df = df_receipt.query('not customer_id.str.startswith("Z")', engine='python')[['customer_id', 'amount']].groupby('customer_id').sum()
qs = df.quantile((0.25, 0.75))
iqr = qs.amount[0.75] - qs.amount[0.25]
th_l = qs.amount[0.25] - iqr * 1.5
th_h = qs.amount[0.75] + iqr * 1.5
outliers = df.query(f'not ({th_l} <= amount <= {th_h})')
outliers.head(10)
```

### P-079

商品データフレーム（df_product）の各項目に対し、欠損数を確認せよ。

```python
(df_product.isnull() | df_product.isna()).sum()
```

### P-080

商品データフレーム（df_product）のいずれかの項目に欠損が発生しているレコードを全て削除した新たなdf_product_1を作成せよ。なお、削除前後の件数を表示させ、前設問で確認した件数だけ減少していることも確認すること。

```python
df_product_1 = df_product.dropna()
print(f'df_product count: {len(df_product)}, df_product_1 count: {len(df_product_1)}')
```

### P-081

単価（unit_price）と原価（unit_cost）の欠損値について、それぞれの平均値で補完した新たなdf_product_2を作成せよ。なお、平均値については1円未満を丸めること（四捨五入または偶数への丸めで良い）。補完実施後、各項目について欠損が生じていないことも確認すること。

```python
df_product_2 = df_product.copy()
df_product_2['unit_price'].fillna(np.round(df_product_2['unit_price'].mean(skipna=True)), inplace=True)
df_product_2['unit_cost'].fillna(np.round(df_product_2['unit_cost'].mean(skipna=True)), inplace=True)
(df_product_2.isnull() | df_product_2.isna()).sum()
```

### P-082

単価（unit_price）と原価（unit_cost）の欠損値について、それぞれの中央値で補完した新たなdf_product_3を作成せよ。なお、中央値については1円未満を丸めること（四捨五入または偶数への丸めで良い）。補完実施後、各項目について欠損が生じていないことも確認すること。

```python
df_product_3 = df_product.copy()
df_product_3['unit_price'].fillna(np.round(df_product_3['unit_price'].median(skipna=True)), inplace=True)
df_product_3['unit_cost'].fillna(np.round(df_product_3['unit_cost'].median(skipna=True)), inplace=True)
(df_product_3.isnull() | df_product_3.isna()).sum()
```

### P-083

単価（unit_price）と原価（unit_cost）の欠損値について、各商品の小区分（category_small_cd）ごとに算出した中央値で補完した新たなdf_product_4を作成せよ。なお、中央値については1円未満を丸めること（四捨五入または偶数への丸めで良い）。補完実施後、各項目について欠損が生じていないことも確認すること。

```python
df_medians = np.round(df_product.groupby('category_small_cd').median())
df_product_nonull = df_product.dropna()
df_product_null = df_product[(df_product.isnull() | df_product.isna()).any(axis=1)]
del(df_product_null['unit_price'])
del(df_product_null['unit_cost'])
df_product_4 = pd.concat((
    df_product_nonull,
    df_product_null.merge(df_medians, on='category_small_cd', how='left')
))
(df_product_4.isna() | df_product_4.isnull()).sum()
```

### P-084

顧客データフレーム（df_customer）の全顧客に対し、全期間の売上金額に占める2019年売上金額の割合を計算せよ。ただし、売上実績がない場合は0として扱うこと。そして計算した割合が0超のものを抽出せよ。 結果は10件表示させれば良い。また、作成したデータにNAやNANが存在しないことを確認せよ。

```python
df = df_customer[['customer_id']].merge(
    df_receipt[['customer_id', 'sales_ymd', 'amount']],
    on='customer_id',
    how='left'
)
df['amount'].fillna(0, inplace=True)
df_amount_all = df[['customer_id', 'amount']].groupby('customer_id').sum()
df_amount_2019 = df.query('20190000 < sales_ymd < 20200000')[['customer_id', 'amount']].groupby('customer_id').sum()
df2 = df_amount_all.merge(df_amount_2019, on='customer_id', how='left')
df2['r2019'] = df2['amount_y'] / df2['amount_x']
df2.fillna(0, inplace=True)
print(df2.query('r2019 > 0').head(10))
(df2.isnull() | df2.isna()).sum()
```

### P-085

顧客データフレーム（df_customer）の全顧客に対し、郵便番号（postal_cd）を用いて経度緯度変換用データフレーム（df_geocode）を紐付け、新たなdf_customer_1を作成せよ。ただし、複数紐づく場合は経度（longitude）、緯度（latitude）それぞれ平均を算出すること。

```python
df_customer_1 = df_customer.merge(
    df_geocode.groupby('postal_cd').mean(),
    on='postal_cd',
    how='left'
)
df_customer_1.head(5)
```

### P-086

前設問で作成した緯度経度つき顧客データフレーム（df_customer_1）に対し、申込み店舗コード（application_store_cd）をキーに店舗データフレーム（df_store）と結合せよ。そして申込み店舗の緯度（latitude）・経度情報（longitude)と顧客の緯度・経度を用いて距離（km）を求め、顧客ID（customer_id）、顧客住所（address）、店舗住所（address）とともに表示せよ。計算式は簡易式で良いものとするが、その他精度の高い方式を利用したライブラリを利用してもかまわない。結果は10件表示すれば良い。

```python
df_store2 = df_store[['store_cd', 'address', 'latitude', 'longitude']] \
  .rename(columns={'store_cd': 'application_store_cd', 'latitude': 'store_latitude', 'longitude': 'store_longitude', 'address': 'store_address'})
df = df_customer_1.merge(
    df_store2,
    on='application_store_cd',
    how='left'
)
df['distance'] = 6371 * np.arccos(
    np.sin(df['latitude'] / 180 * np.pi) * np.sin(df['store_latitude'] / 180 * np.pi) +
    np.cos(df['latitude'] / 180 * np.pi) * np.cos(df['store_latitude'] / 180 * np.pi) *
    np.cos(df['longitude'] / 180 * np.pi - df['store_longitude'] / 180 * np.pi)
)
df[['customer_id', 'address', 'store_address', 'distance']].head()
```

### P-087

顧客データフレーム（df_customer）では、異なる店舗での申込みなどにより同一顧客が複数登録されている。名前（customer_name）と郵便番号（postal_cd）が同じ顧客は同一顧客とみなし、1顧客1レコードとなるように名寄せした名寄顧客データフレーム（df_customer_u）を作成せよ。ただし、同一顧客に対しては売上金額合計が最も高いものを残すものとし、売上金額合計が同一もしくは売上実績がない顧客については顧客ID（customer_id）の番号が小さいものを残すこととする。

```python
df_amount = df_receipt[['customer_id', 'amount']].groupby('customer_id').sum()
df_customer_u = df_customer.merge(df_amount, on='customer_id', how='left')
df_customer_u['amount'].fillna(0, inplace=True)
df_customer_u.sort_values(['amount', 'customer_id'], ascending=[False, True], inplace=True)
df_customer_u.drop_duplicates(keep='first', subset=['customer_name', 'postal_cd'], inplace=True)
```

### P-088

前設問で作成したデータを元に、顧客データフレームに統合名寄IDを付与したデータフレーム（df_customer_n）を作成せよ。ただし、統合名寄IDは以下の仕様で付与するものとする。

* 重複していない顧客：顧客ID（customer_id）を設定
* 重複している顧客：前設問で抽出したレコードの顧客IDを設定

```python
df = df_customer_u[['customer_name', 'postal_cd', 'customer_id']].rename(columns={'customer_id': 'customer_id_n'})
df_customer_n = df_customer.merge(df, on=['customer_name', 'postal_cd'], how='left')
df_customer_n.head(10)
```

### P-閑話

df_customer_1, df_customer_nは使わないので削除する。

```Python
del(df_customer_1)
del(df_customer_n)
```

### P-089

売上実績がある顧客に対し、予測モデル構築のため学習用データとテスト用データに分割したい。それぞれ8:2の割合でランダムにデータを分割せよ。

```python
df = df_customer.merge(
    df_receipt[['customer_id', 'amount']].groupby('customer_id').sum(),
    on='customer_id',
    how='left'
)
customer_with_sales = df.query('amount > 0')
train_data, test_data = train_test_split(customer_with_sales, test_size=0.2)
```

### P-090

レシート明細データフレーム（df_receipt）は2017年1月1日〜2019年10月31日までのデータを有している。売上金額（amount）を月次で集計し、学習用に12ヶ月、テスト用に6ヶ月のモデル構築用データを3セット作成せよ。

```python
何をするモデルを構築するのか不明であり、解答不能
```

### P-091

顧客データフレーム（df_customer）の各顧客に対し、売上実績がある顧客数と売上実績がない顧客数が1:1となるようにアンダーサンプリングで抽出せよ。

```python
df = df_customer.merge(
    df_receipt[['customer_id', 'amount']].groupby('customer_id').sum(),
    on='customer_id',
    how='left'
)
df['amount'].fillna(0, inplace=True)
customer_with_sales = df.query('amount > 0')
customer_without_sales = df.query('amount == 0')
sample_size = min(len(customer_with_sales), len(customer_without_sales))
pd.concat((
    customer_with_sales.sample(sample_size),
    customer_without_sales.sample(sample_size)
))
```

### P-092

顧客データフレーム（df_customer）では、性別に関する情報が非正規化の状態で保持されている。これを第三正規化せよ。

```python
df_gender = df_customer[['gender_cd', 'gender']].drop_duplicates()
del(df_customer['gender'])
```

### P-093

商品データフレーム（df_product）では各カテゴリのコード値だけを保有し、カテゴリ名は保有していない。カテゴリデータフレーム（df_category）と組み合わせて非正規化し、カテゴリ名を保有した新たな商品データフレームを作成せよ。

```python
df_product_2 = df_product.merge(
    df_category,
    on=['category_major_cd', 'category_medium_cd', 'category_small_cd'],
    how='left'
)
```

### P-094

先に作成したカテゴリ名付き商品データを以下の仕様でファイル出力せよ。なお、出力先のパスはdata配下とする。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ有り
* 文字コードはUTF-8


```python
df_product_2.to_csv('data/products_2.csv', header=True, encoding='UTF-8')
```

### P-095

先に作成したカテゴリ名付き商品データを以下の仕様でファイル出力せよ。なお、出力先のパスはdata配下とする。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ有り
* 文字コードはCP932

```python
df_product_2.to_csv('data/products_2.csv', header=True, encoding='CP932')
```

### P-096

先に作成したカテゴリ名付き商品データを以下の仕様でファイル出力せよ。なお、出力先のパスはdata配下とする。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ無し
* 文字コードはUTF-8

```python
df_product_2.to_csv('data/products_2.csv', header=True, encoding='UTF-8')
```

### P-097

先に作成した以下形式のファイルを読み込み、データフレームを作成せよ。また、先頭3件を表示させ、正しくとりまれていることを確認せよ。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ有り
* 文字コードはUTF-8


```python
pd.read_csv('data/products_2.csv', header=0, encoding='UTF-8').head(3)
```

### P-098

先に作成した以下形式のファイルを読み込み、データフレームを作成せよ。また、先頭3件を表示させ、正しくとりまれていることを確認せよ。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ無し
* 文字コードはUTF-8

```python
pd.read_csv('data/products_2.csv', header=None, encoding='UTF-8').head(3)
```

### P-099

先に作成したカテゴリ名付き商品データを以下の仕様でファイル出力せよ。なお、出力先のパスはdata配下とする。

* ファイル形式はTSV（タブ区切り）
* ヘッダ有り
* 文字コードはUTF-8

```python
df_product_2.to_csv('data/products_2.tsv', quotechar='\t', header=True, encoding='UTF-8')
```

### P-100

先に作成した以下形式のファイルを読み込み、データフレームを作成せよ。また、先頭3件を表示させ、正しくとりまれていることを確認せよ。

* ファイル形式はTSV（タブ区切り）
* ヘッダ有り
* 文字コードはUTF-8

```python
pd.read_csv('data/products_2.tsv', quotechar='\t', header=0, encoding='UTF-8').head(3)
```
