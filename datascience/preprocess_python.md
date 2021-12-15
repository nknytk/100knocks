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
