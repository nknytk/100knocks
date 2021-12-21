# データサイエンス100本ノック（構造化データ加工編） - SQL

## S-001

レシート明細テーブル（receipt）から全項目の先頭10件を表示し、どのようなデータを保有しているか目視で確認せよ。

```SQL
SELECT * FROM receipt LIMIT 10
```

### S-002

レシート明細のテーブル（receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、10件表示させよ。

```SQL
SELECT sales_ymd, customer_id, product_cd, amount FROM receipt LIMIT 10
```

### S-003

レシート明細のテーブル（receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、10件表示させよ。ただし、sales_ymdはsales_dateに項目名を変更しながら抽出すること。

```SQL
SELECT sales_ymd AS sales_date, customer_id, product_cd, amount FROM receipt LIMIT 10
```

### S-004

レシート明細のテーブル（receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"

```SQL
SELECT sales_ymd, customer_id, product_cd, amount FROM receipt WHERE customer_id = 'CS018205000001'
```

### S-005

レシート明細のテーブル（receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"
* 売上金額（amount）が1,000以上

```SQL
SELECT sales_ymd, customer_id, product_cd, amount FROM receipt WHERE customer_id = 'CS018205000001' AND amount >= 1000
```

### S-006

レシート明細テーブル（receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上数量（quantity）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"
* 売上金額（amount）が1,000以上または売上数量（quantity）が5以上

```SQL
SELECT sales_ymd, customer_id, product_cd, amount
FROM receipt
WHERE customer_id = 'CS018205000001'
  AND (amount >= 1000 or quantity >= 5)
```

### S-007

レシート明細のテーブル（receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"
* 売上金額（amount）が1,000以上2,000以下

```python
SELECT sales_ymd, customer_id, product_cd, amount
FROM receipt
WHERE customer_id = 'CS018205000001'
  AND amount BETWEEN 1000 AND 2000
```

### S-008

レシート明細テーブル（receipt）から売上日（sales_ymd）、顧客ID（customer_id）、商品コード（product_cd）、売上金額（amount）の順に列を指定し、以下の条件を満たすデータを抽出せよ。

* 顧客ID（customer_id）が"CS018205000001"
* 商品コード（product_cd）が"P071401019"以外

```SQL
SELECT sales_ymd, customer_id, product_cd, amount
FROM receipt
WHERE customer_id = 'CS018205000001' AND product_cd != 'P071401019'
```

### S-009

以下の処理において、出力結果を変えずにORをANDに書き換えよ

```SQL
select * from store where prefecture_cd != '13' AND floor_area <= 900
```

### S-010

店舗テーブル（store）から、店舗コード（store_cd）が"S14"で始まるものだけ全項目抽出し、10件だけ表示せよ

```SQL
SELECT * FROM store WHERE store_cd LIKE 'S14%' LIMIT 10
```

### S-011

顧客テーブル（customer）から顧客ID（customer_id）の末尾が1のものだけ全項目抽出し、10件だけ表示せよ。

```SQL
SELECT * FROM customer WHERE customer_id LIKE '%1' LIMIT 10
```

### S-012

店舗テーブル（store）から横浜市の店舗だけ全項目表示せよ。

```SQL
SELECT * FROM store WHERE address LIKE '%横浜市%'
```

### S-013

顧客テーブル（customer）から、ステータスコード（status_cd）の先頭がアルファベットのA〜Fで始まるデータを全項目抽出し、10件だけ表示せよ。

```SQL
SELECT * FROM customer WHERE status_cd ~ '^[A-F].*$' LIMIT 10
```

### S-014

顧客テーブル（customer）から、ステータスコード（status_cd）の末尾が数字の1〜9で終わるデータを全項目抽出し、10件だけ表示せよ。

```SQL
SELECT * FROM customer WHERE status_cd ~ '^.*[1-9]$' LIMIT 10
```

### S-015

顧客テーブル（customer）から、ステータスコード（status_cd）の先頭がアルファベットのA〜Fで始まり、末尾が数字の1〜9で終わるデータを全項目抽出し、10件だけ表示せよ。

```SQL
SELECT * FROM customer WHERE status_cd ~ '^[A-F].*[1-9]' LIMIT 10
```

### S-016

店舗テーブル（store）から、電話番号（tel_no）が3桁-3桁-4桁のデータを全項目表示せよ。

```SQL
SELECT * FROM store WHERE tel_no ~ '^\d{3}-\d{3}-\d{4}$'
```

### S-017

顧客テーブル（customer）を生年月日（birth_day）で高齢順にソートし、先頭10件を全項目表示せよ。

```SQL
SELECT * FROM customer ORDER BY birth_day ASC LIMIT 10
```

### S-018

顧客テーブル（customer）を生年月日（birth_day）で若い順にソートし、先頭10件を全項目表示せよ。

```SQL
SELECT * FROM customer ORDER BY birth_day DESC LIMIT 10
```

### S-019

レシート明細テーブル（receipt）に対し、1件あたりの売上金額（amount）が高い順にランクを付与し、先頭10件を抽出せよ。項目は顧客ID（customer_id）、売上金額（amount）、付与したランクを表示させること。なお、売上金額（amount）が等しい場合は同一順位を付与するものとする。

```SQL
SELECT RANK() OVER (ORDER BY amount DESC) AS rank, *
FROM receipt
ORDER BY amount
DESC LIMIT 10
```

### S-020

レシート明細テーブル（receipt）に対し、1件あたりの売上金額（amount）が高い順にランクを付与し、先頭10件を抽出せよ。項目は顧客ID（customer_id）、売上金額（amount）、付与したランクを表示させること。なお、売上金額（amount）が等しい場合でも別順位を付与すること。

```SQL
SELECT RANK() OVER (ORDER BY amount DESC, customer_id ASC) AS rank, *
FROM receipt
ORDER BY amount
DESC LIMIT 10
```

### S-021

レシート明細テーブル（receipt）に対し、件数をカウントせよ

```SQL
SELECT COUNT(1) FROM receipt
```

### S-022

レシート明細テーブル（receipt）の顧客ID（customer_id）に対し、ユニーク件数をカウントせよ。

```SQL
SELECT COUNT(DISTINCT(customer_id)) FROM receipt
```

### S-023

レシート明細テーブル（receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）と売上数量（quantity）を合計せよ。

```SQL
SELECT store_cd, SUM(amount), SUM(quantity) FROM receipt GROUP BY store_cd LIMIT 10
```

### S-024

レシート明細テーブル（receipt）に対し、顧客ID（customer_id）ごとに最も新しい売上日（sales_ymd）を求め、10件表示せよ。

```SQL
SELECT customer_id, MAX(sales_ymd) FROM receipt GROUP BY customer_id LIMIT 10
```

### S-025

レシート明細テーブル（receipt）に対し、顧客ID（customer_id）ごとに最も古い売上日（sales_ymd）を求め、10件表示せよ。

```SQL
SELECT customer_id, MIN(sales_ymd) FROM receipt GROUP BY customer_id LIMIT 10
```

### S-026

レシート明細テーブル（receipt）に対し、顧客ID（customer_id）ごとに最も新しい売上日（sales_ymd）と古い売上日を求め、両者が異なるデータを10件表示せよ。

```SQL
SELECT customer_id, MIN(sales_ymd), MAX(sales_ymd) FROM receipt GROUP BY customer_id LIMIT 10
```

### S-027

レシート明細テーブル（receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の平均を計算し、降順でTOP5を表示せよ。

```SQL
SELECT store_cd, AVG(amount) AS avg_amount FROM receipt GROUP BY store_cd ORDER BY avg_amount DESC LIMIT 5
```

### S-028

レシート明細テーブル（receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の中央値を計算し、降順でTOP5を表示せよ

```SQL
SELECT store_cd, PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY amount) AS mid_amount
FROM receipt
GROUP BY store_cd
ORDER BY mid_amount DESC
LIMIT 5
```

### S-029

レシート明細テーブル（receipt）に対し、店舗コード（store_cd）ごとに商品コード（product_cd）の最頻値を求めよ。

```SQL
WITH t AS (
  SELECT store_cd, product_cd, COUNT(1) AS prd_cnt
  FROM receipt
  GROUP BY store_cd, product_cd
)
SELECT store_cd, product_cd, prd_cnt
FROM (
  SELECT store_cd, product_cd, prd_cnt, RANK() OVER (PARTITION BY store_cd ORDER BY prd_cnt DESC) AS r 
  FROM t
) t2
WHERE r = 1
LIMIT 5
```

### S-030

レシート明細テーブル（receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の標本分散を計算し、降順でTOP5を表示せよ。

```SQL
SELECT store_cd, VAR_SAMP(amount) AS v FROM receipt GROUP BY store_cd ORDER BY v DESC LIMIT 5
```

### S-031

レシート明細テーブル（receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の標本標準偏差を計算し、降順でTOP5を表示せよ。

```SQL
SELECT store_cd, STDDEV_SAMP(amount) AS std FROM receipt GROUP BY store_cd ORDER BY std DESC LIMIT 5
```

### S-032

レシート明細テーブル（receipt）の売上金額（amount）について、25％刻みでパーセンタイル値を求めよ。

```SQL
SELECT
  PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY amount),
  PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY amount),
  PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY amount)
FROM receipt
```

### S-033

レシート明細テーブル（receipt）に対し、店舗コード（store_cd）ごとに売上金額（amount）の平均を計算し、330以上のものを抽出せよ。

```SQL
WITH t AS (
  SELECT store_cd, AVG(amount) AS avg_amount FROM receipt GROUP BY store_cd
)
SELECT store_cd, avg_amount FROM t WHERE avg_amount >= 330 LIMIT 10
```

### S-034

レシート明細テーブル（receipt）に対し、顧客ID（customer_id）ごとに売上金額（amount）を合計して全顧客の平均を求めよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。

```SQL
WITH t AS (
  SELECT customer_id, SUM(amount) AS sum_amount
  FROM receipt 
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
)
SELECT AVG(sum_amount) FROM t
```

### S-035

レシート明細テーブル（receipt）に対し、顧客ID（customer_id）ごとに売上金額（amount）を合計して全顧客の平均を求め、平均以上に買い物をしている顧客を抽出せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。なお、データは10件だけ表示させれば良い。

```SQL
WITH t AS (
  SELECT customer_id, SUM(amount) AS sum_amount
  FROM receipt 
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
)
SELECT customer_id, sum_amount
FROM t
WHERE sum_amount >= (SELECT AVG(sum_amount) FROM t)
LIMIT 10
```

### S-036

レシート明細テーブル（receipt）と店舗テーブル（store）を内部結合し、レシート明細テーブルの全項目と店舗テーブルの店舗名（store_name）を10件表示させよ。

```SQL
SELECT receipt.*, store_name
FROM receipt
LEFT JOIN store
ON receipt.store_cd = store.store_cd
LIMIT 10
```

### S-037

商品テーブル（product）とカテゴリテーブル（category）を内部結合し、商品テーブルの全項目とカテゴリテーブルの小区分名（category_small_name）を10件表示させよ。

```SQL
SELECT product.*, category_small_name
FROM product
LEFT JOIN category
ON product.category_major_cd = category.category_major_cd
  AND product.category_medium_cd = category.category_medium_cd
  AND product.category_small_cd = category.category_small_cd
LIMIT 10
```

### S-038

顧客テーブル（customer）とレシート明細テーブル（receipt）から、各顧客ごとの売上金額合計を求めよ。ただし、売上実績がない顧客については売上金額を0として表示させること。また、顧客は性別コード（gender_cd）が女性（1）であるものを対象とし、非会員（顧客IDが"Z"から始まるもの）は除外すること。なお、結果は10件だけ表示させれば良い。

```SQL
WITH t AS (
  SELECT customer_id, SUM(amount) AS sum_amount
  FROM receipt 
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
)
SELECT
  customer.customer_id,
  CASE WHEN t.sum_amount IS NULL THEN 0 ELSE t.sum_amount END
FROM customer
LEFT JOIN t
ON customer.customer_id = t.customer_id
LIMIT 10
```

### S-039

レシート明細テーブル（receipt）から売上日数の多い顧客の上位20件と、売上金額合計の多い顧客の上位20件を抽出し、完全外部結合せよ。ただし、非会員（顧客IDが"Z"から始まるもの）は除外すること。

```SQL
WITH t AS (
  SELECT customer_id, SUM(amount) AS sum_amount, SUM(DISTINCT(sales_ymd)) AS n_days
  FROM receipt 
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
)

SELECT * FROM (SELECT * FROM t ORDER BY sum_amount DESC LIMIT 20) t1
LEFT OUTER JOIN (SELECT * FROM t ORDER BY n_days DESC LIMIT 20) t2
ON t1.customer_id = t2.customer_id
```

### S-040

全ての店舗と全ての商品を組み合わせると何件のデータとなるか調査したい。店舗（store）と商品（product）を直積した件数を計算せよ。

```SQL
SELECT (SELECT COUNT(1) FROM store) * (SELECT COUNT(1) FROM product)
```

### S-041

レシート明細テーブル（receipt）の売上金額（amount）を日付（sales_ymd）ごとに集計し、前日からの売上金額増減を計算せよ。なお、計算結果は10件表示すればよい。

```SQL
WITH t AS (
  SELECT sales_ymd, SUM(amount) AS sum_amount
  FROM receipt
  GROUP BY sales_ymd
)
SELECT
  sales_ymd,
  sum_amount,
  LAG(sum_amount) OVER (ORDER BY sales_ymd DESC) AS sum_amount_1,
  sum_amount - LAG(sum_amount) OVER (ORDER BY sales_ymd DESC) AS diff
FROM t
LIMIT 10
```

### S-042

レシート明細テーブル（receipt）の売上金額（amount）を日付（sales_ymd）ごとに集計し、各日付のデータに対し、１日前、２日前、３日前のデータを結合せよ。結果は10件表示すればよい。

```SQL
WITH t AS (
  SELECT sales_ymd, SUM(amount) AS sum_amount
  FROM receipt
  GROUP BY sales_ymd
)
SELECT
  sales_ymd,
  sum_amount,
  LAG(sum_amount) OVER (ORDER BY sales_ymd DESC) AS sum_amount_1,
  LAG(sum_amount, 2) OVER (ORDER BY sales_ymd DESC) AS sum_amount_2,
  LAG(sum_amount, 3) OVER (ORDER BY sales_ymd DESC) AS sum_amount_3
FROM t
LIMIT 10
```

### S-043

レシート明細テーブル（receipt）と顧客テーブル（customer）を結合し、性別（gender）と年代（ageから計算）ごとに売上金額（amount）を合計した売上サマリテーブル（sales_summary）を作成せよ。性別は0が男性、1が女性、9が不明を表すものとする。

ただし、項目構成は年代、女性の売上金額、男性の売上金額、性別不明の売上金額の4項目とすること（縦に年代、横に性別のクロス集計）。また、年代は10歳ごとの階級とすること。

```SQL
WITH t AS (
  SELECT amount, gender_cd, age / 10 AS era
  FROM receipt
  INNER JOIN customer
  ON receipt.customer_id = customer.customer_id
)
SELECT
  era,
  SUM(CASE WHEN gender_cd = '0' THEN amount ELSE 0 END) AS male_sales,
  SUM(CASE WHEN gender_cd = '1' THEN amount ELSE 0 END) AS female_sales,
  SUM(CASE WHEN gender_cd = '9' THEN amount ELSE 0 END) AS unknown_sales
FROM t
GROUP BY era
```

### S-044

前設問で作成した売上サマリテーブル（sales_summary）は性別の売上を横持ちさせたものであった。このテーブルから性別を縦持ちさせ、年代、性別コード、売上金額の3項目に変換せよ。ただし、性別コードは男性を"00"、女性を"01"、不明を"99"とする。

```SQL
WITH t AS (
  SELECT
    amount,
    CASE WHEN gender_cd = '0' THEN '00'
         WHEN gender_cd = '1' THEN '01'
         WHEN gender_cd = '9' THEN '99'
    END AS gender,
    age / 10 AS era
  FROM receipt
  INNER JOIN customer
  ON receipt.customer_id = customer.customer_id
)
SELECT era, gender, SUM(amount)
FROM t
GROUP BY era, gender
```

### S-045

顧客テーブル（customer）の生年月日（birth_day）は日付型でデータを保有している。これをYYYYMMDD形式の文字列に変換し、顧客ID（customer_id）とともに抽出せよ。データは10件を抽出すれば良い。

```SQL
SELECT customer_id, TO_CHAR(birth_day, 'YYYYMMDD') FROM customer LIMIT 10
```

### S-046

顧客テーブル（customer）の申し込み日（application_date）はYYYYMMDD形式の文字列型でデータを保有している。これを日付型に変換し、顧客ID（customer_id）とともに抽出せよ。データは10件を抽出すれば良い。

```SQL
SELECT customer_id, TO_DATE(application_date, 'YYYYMMDD') FROM customer LIMIT 10
```

### S-047

レシート明細テーブル（receipt）の売上日（sales_ymd）はYYYYMMDD形式の数値型でデータを保有している。これを日付型に変換し、レシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。データは10件を抽出すれば良い。

```SQL
SELECT receipt_no, receipt_sub_no, TO_DATE(CAST(sales_ymd AS TEXT), 'YYYYMMDD') FROM receipt LIMIT 10
```

### S-048

レシート明細テーブル（receipt）の売上エポック秒（sales_epoch）は数値型のUNIX秒でデータを保有している。これを日付型に変換し、レシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。データは10件を抽出すれば良い。

```SQL
SELECT receipt_no, receipt_sub_no, TO_TIMESTAMP(sales_epoch) FROM receipt LIMIT 10
```

### S-049

レシート明細テーブル（receipt）の販売エポック秒（sales_epoch）を日付型に変換し、「年」だけ取り出してレシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。データは10件を抽出すれば良い。

```SQL
SELECT receipt_no, receipt_sub_no, TO_CHAR(TO_TIMESTAMP(sales_epoch), 'YYYY') FROM receipt LIMIT 10
```

### S-050

レシート明細テーブル（receipt）の売上エポック秒（sales_epoch）を日付型に変換し、「月」だけ取り出してレシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。なお、「月」は0埋め2桁で取り出すこと。データは10件を抽出すれば良い。

```SQL
SELECT receipt_no, receipt_sub_no, TO_CHAR(TO_TIMESTAMP(sales_epoch), 'MM') FROM receipt LIMIT 10
```

### S-051

レシート明細テーブル（receipt）の売上エポック秒を日付型に変換し、「日」だけ取り出してレシート番号(receipt_no)、レシートサブ番号（receipt_sub_no）とともに抽出せよ。なお、「日」は0埋め2桁で取り出すこと。データは10件を抽出すれば良い。

```SQL
SELECT receipt_no, receipt_sub_no, TO_CHAR(TO_TIMESTAMP(sales_epoch), 'DD') FROM receipt LIMIT 10
```

### S-052

レシート明細テーブル（receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計の上、売上金額合計に対して2,000円以下を0、2,000円より大きい金額を1に2値化し、顧客ID、売上金額合計とともに10件表示せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。

```SQL
SELECT customer_id, CAST(SUM(amount) >= 2000 AS INTEGER)
FROM receipt
WHERE NOT customer_id LIKE 'Z%'
GROUP BY customer_id
LIMIT 10
```

### S-053

顧客テーブル（customer）の郵便番号（postal_cd）に対し、東京（先頭3桁が100〜209のもの）を1、それ以外のものを0に２値化せよ。さらにレシート明細テーブル（receipt）と結合し、全期間において売上実績がある顧客数を、作成した2値ごとにカウントせよ。

```SQL
WITH t AS (
  SELECT customer_id, CAST(CAST(SUBSTR(postal_cd, 0, 4) AS INTEGER) BETWEEN 100 AND 209 AS INTEGER) AS is_tokyo
  FROM customer
)
SELECT is_tokyo, COUNT(DISTINCT(customer_id)) AS n_customers
FROM (
  SELECT receipt.customer_id, is_tokyo
  FROM receipt
  LEFT JOIN t
  ON receipt.customer_id = t.customer_id
) t1
GROUP BY is_tokyo
```

### S-054

顧客テーブル（customer）の住所（address）は、埼玉県、千葉県、東京都、神奈川県のいずれかとなっている。都道府県毎にコード値を作成し、顧客ID、住所とともに抽出せよ。値は埼玉県を11、千葉県を12、東京都を13、神奈川県を14とすること。結果は10件表示させれば良い

```SQL
SELECT
  customer_id,
  address,
  CASE WHEN address ~ '^埼玉県.*$' THEN 11
       WHEN address ~ '^千葉県.*$' THEN 12
       WHEN address ~ '^東京都.*$' THEN 13
       WHEN address ~ '^神奈川県.*$' THEN 14
  END AS pref_cd
FROM customer
LIMIT 10
```

### S-055

レシート明細テーブル（receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、その合計金額の四分位点を求めよ。その上で、顧客ごとの売上金額合計に対して以下の基準でカテゴリ値を作成し、顧客ID、売上金額合計とともに表示せよ。カテゴリ値は上から順に1〜4とする。結果は10件表示させれば良い。

* 最小値以上第一四分位未満
* 第一四分位以上第二四分位未満
* 第二四分位以上第三四分位未満
* 第三四分位以上

```SQL
WITH t AS (
  SELECT customer_id, SUM(amount) AS sum_amount
  FROM receipt
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
),
t2 AS (
  SELECT
    PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY sum_amount) AS th4,
    PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY sum_amount) AS th3,
    PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY sum_amount) AS th2
  FROM t
)
SELECT
  customer_id,
  sum_amount,
  CASE WHEN sum_amount >= (SELECT th4 FROM t2) THEN 4
       WHEN sum_amount >= (SELECT th3 FROM t2) THEN 3
       WHEN sum_amount >= (SELECT th2 FROM t2) THEN 2
       ELSE 1
  END AS amount_category
FROM t
LIMIT 10
```

### S-056

顧客テーブル（customer）の年齢（age）をもとに10歳刻みで年代を算出し、顧客ID（customer_id）、生年月日（birth_day）とともに抽出せよ。ただし、60歳以上は全て60歳代とすること。年代を表すカテゴリ名は任意とする。先頭10件を表示させればよい。

```SQL
SELECT
  customer_id,
  birth_day,
  CASE WHEN age >= 60 THEN 60 ELSE age / 10 * 10 END AS era
FROM customer
LIMIT 10
```

### S-057

前問題の抽出結果と性別（gender）を組み合わせ、新たに性別×年代の組み合わせを表すカテゴリデータを作成せよ。組み合わせを表すカテゴリの値は任意とする。先頭10件を表示させればよい。

```SQL
SELECT
  customer_id,
  birth_day,
  CONCAT_WS('_', gender, CASE WHEN age >= 60 THEN 60 ELSE age / 10 * 10 END) AS gender_era
FROM customer
LIMIT 10
```

### S-058

顧客テーブル（customer）の性別コード（gender_cd）をダミー変数化し、顧客ID（customer_id）とともに抽出せよ。結果は10件表示させれば良い。

```SQL
SELECT
  customer_id,
  CAST(gender_cd = '0' AS INTEGER) AS gender_0,
  CAST(gender_cd = '1' AS INTEGER) AS gender_1,
  CAST(gender_cd = '99' AS INTEGER) AS gender_99
FROM customer
LIMIT 10
```

### S-059

レシート明細テーブル（receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、売上金額合計を平均0、標準偏差1に標準化して顧客ID、売上金額合計とともに表示せよ。標準化に使用する標準偏差は、不偏標準偏差と標本標準偏差のどちらでも良いものとする。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。結果は10件表示させれば良い。

```SQL
WITH t AS (
  SELECT customer_id, SUM(amount) AS sum_amount
  FROM receipt
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
),
t2 AS (
  SELECT AVG(sum_amount) AS avg_amount, STDDEV_SAMP(sum_amount) AS stddev_amount FROM t
)
SELECT
  customer_id,
  sum_amount,
  (sum_amount - (SELECT avg_amount FROM t2)) / (SELECT stddev_amount FROM t2) AS norm_amount
FROM t
LIMIT 10
```

### S-060

レシート明細テーブル（receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、売上金額合計を最小値0、最大値1に正規化して顧客ID、売上金額合計とともに表示せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。結果は10件表示させれば良い

```SQL
WITH t AS (
  SELECT customer_id, CAST(SUM(amount) AS FLOAT) AS sum_amount
  FROM receipt
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
),
t2 AS (
  SELECT MIN(sum_amount) AS min_amount, MAX(sum_amount), MAX(sum_amount) - MIN(sum_amount) AS range_amount
  FROM t
)
SELECT
  customer_id,
  sum_amount,
  (sum_amount - (SELECT min_amount FROM t2)) / (SELECT range_amount FROM t2) AS norm_amount
FROM t
LIMIT 10
```

### S-061

レシート明細テーブル（receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、売上金額合計を常用対数化（底=10）して顧客ID、売上金額合計とともに表示せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。結果は10件表示させれば良い。

```SQL
SELECT customer_id, SUM(amount) AS sum_amount, LOG(10, SUM(amount)) AS log10_amount
FROM receipt
WHERE NOT customer_id LIKE 'Z%'
GROUP BY customer_id
LIMIT 10
```

### S-062

レシート明細テーブル（receipt）の売上金額（amount）を顧客ID（customer_id）ごとに合計し、売上金額合計を自然対数化(底=e）して顧客ID、売上金額合計とともに表示せよ（ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること）。結果は10件表示させれば良い。

```SQL
SELECT customer_id, SUM(amount) AS sum_amount, LN(SUM(amount)) AS log10_amount
FROM receipt
WHERE NOT customer_id LIKE 'Z%'
GROUP BY customer_id
LIMIT 10
```

### S-063

商品テーブル（product）の単価（unit_price）と原価（unit_cost）から、各商品の利益額を算出せよ。結果は10件表示させれば良い。

```SQL
SELECT product_cd, unit_price - unit_cost AS profit FROM product LIMIT 10
```

### S-064

商品テーブル（product）の単価（unit_price）と原価（unit_cost）から、各商品の利益率の全体平均を算出せよ。 ただし、単価と原価にはNULLが存在することに注意せよ。

```SQL
SELECT AVG(unit_price - unit_cost)
FROM product
WHERE unit_price IS NOT NULL AND unit_cost IS NOT NULL
```

### S-065

商品テーブル（product）の各商品について、利益率が30%となる新たな単価を求めよ。ただし、1円未満は切り捨てること。そして結果を10件表示させ、利益率がおよそ30％付近であることを確認せよ。ただし、単価（unit_price）と原価（unit_cost）にはNULLが存在することに注意せよ。

```SQL
SELECT
  product_cd,
  unit_price,
  unit_cost,
  FLOOR(CAST(unit_cost AS FLOAT) / 0.7) AS p30_price,
  (FLOOR(CAST(unit_cost AS FLOAT) / 0.7) - unit_cost) / FLOOR(CAST(unit_cost AS FLOAT) / 0.7) AS p30
FROM product
LIMIT 10
```

### S-066

商品テーブル（product）の各商品について、利益率が30%となる新たな単価を求めよ。今回は、1円未満を丸めること（四捨五入または偶数への丸めで良い）。そして結果を10件表示させ、利益率がおよそ30％付近であることを確認せよ。ただし、単価（unit_price）と原価（unit_cost）にはNULLが存在することに注意せよ。

```SQL
SELECT
  product_cd,
  unit_price,
  unit_cost,
  ROUND(CAST(unit_cost AS FLOAT) / 0.7) AS p30_price,
  (ROUND(CAST(unit_cost AS FLOAT) / 0.7) - unit_cost) / ROUND(CAST(unit_cost AS FLOAT) / 0.7) AS p30
FROM product
LIMIT 10
```

### S-067

商品テーブル（product）の各商品について、利益率が30%となる新たな単価を求めよ。今回は、1円未満を切り上げること。そして結果を10件表示させ、利益率がおよそ30％付近であることを確認せよ。ただし、単価（unit_price）と原価（unit_cost）にはNULLが存在することに注意せよ

```SQL
SELECT
  product_cd,
  unit_price,
  unit_cost,
  CEIL(CAST(unit_cost AS FLOAT) / 0.7) AS p30_price,
  (CEIL(CAST(unit_cost AS FLOAT) / 0.7) - unit_cost) / CEIL(CAST(unit_cost AS FLOAT) / 0.7) AS p30
FROM product
LIMIT 10
```

### S-068

商品テーブル（product）の各商品について、消費税率10%の税込み金額を求めよ。 1円未満の端数は切り捨てとし、結果は10件表示すれば良い。ただし、単価（unit_price）にはNULLが存在することに注意せよ。

```SQL
SELECT product_cd, unit_price, FLOOR(unit_price * 1.1) AS price_include_tax FROM product LIMIT 10
```

### S-069

レシート明細テーブル（receipt）と商品テーブル（product）を結合し、顧客毎に全商品の売上金額合計と、カテゴリ大区分（category_major_cd）が"07"（瓶詰缶詰）の売上金額合計を計算の上、両者の比率を求めよ。抽出対象はカテゴリ大区分"07"（瓶詰缶詰）の売上実績がある顧客のみとし、結果は10件表示させればよい。

```SQL
WITH t AS (
  SELECT
    customer_id,
    SUM(amount) AS total_amount,
    SUM(CASE WHEN category_major_cd = '07' THEN amount ELSE 0 END) AS category07_amount,
    SUM(CASE WHEN category_major_cd = '07' THEN CAST(amount AS FLOAT) ELSE 0 END) / SUM(amount) AS category07_ratio
  FROM receipt
  LEFT JOIN product
  ON receipt.product_cd = product.product_cd
  GROUP BY customer_id
)
SELECT * FROM t WHERE category07_amount > 0 LIMIT 10
```

### S-070

レシート明細テーブル（receipt）の売上日（sales_ymd）に対し、顧客テーブル（customer）の会員申込日（application_date）からの経過日数を計算し、顧客ID（customer_id）、売上日、会員申込日とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値、application_dateは文字列でデータを保持している点に注意）。

```SQL
SELECT
  receipt.customer_id,
  sales_ymd,
  application_date,
  TO_DATE(CAST(sales_ymd AS TEXT), 'YYYYMMDD') - TO_DATE(application_date, 'YYYYMMDD') AS elapsed_days
FROM receipt
LEFT JOIN customer
ON receipt.customer_id = customer.customer_id
LIMIT 10
```

### S-071

レシート明細テーブル（receipt）の売上日（sales_ymd）に対し、顧客テーブル（customer）の会員申込日（application_date）からの経過月数を計算し、顧客ID（customer_id）、売上日、会員申込日とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値、application_dateは文字列でデータを保持している点に注意）。1ヶ月未満は切り捨てること。

```SQL
SELECT
  receipt.customer_id,
  sales_ymd,
  application_date,
  (sales_ymd / 10000 - CAST(SUBSTR(application_date, 0, 5) AS INTEGER)) * 12 + (sales_ymd / 100 % 100 - CAST(SUBSTR(application_date, 5, 2) AS INTEGER)) AS elapsed_months 
FROM receipt
LEFT JOIN customer
ON receipt.customer_id = customer.customer_id
LIMIT 10
```

### S-072

レシート明細テーブル（receipt）の売上日（sales_ymd）に対し、顧客テーブル（customer）の会員申込日（application_date）からの経過年数を計算し、顧客ID（customer_id）、売上日、会員申込日とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値、application_dateは文字列でデータを保持している点に注意）。1年未満は切り捨てること。

```SQL
SELECT
  receipt.customer_id,
  sales_ymd,
  application_date,
  sales_ymd / 10000 - CAST(SUBSTR(application_date, 0, 5) AS INTEGER) AS elapsed_years
FROM receipt
LEFT JOIN customer
ON receipt.customer_id = customer.customer_id
LIMIT 10
```

### S-073

レシート明細テーブル（receipt）の売上日（sales_ymd）に対し、顧客テーブル（customer）の会員申込日（application_date）からのエポック秒による経過時間を計算し、顧客ID（customer_id）、売上日、会員申込日とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値、application_dateは文字列でデータを保持している点に注意）。なお、時間情報は保有していないため各日付は0時0分0秒を表すものとする。

```SQL
SELECT
  receipt.customer_id,
  sales_ymd,
  application_date,
  (TO_DATE(CAST(sales_ymd AS TEXT), 'YYYYMMDD') - TO_DATE(application_date, 'YYYYMMDD')) * 24 * 3600 AS elapsed_epoch
FROM receipt
LEFT JOIN customer
ON receipt.customer_id = customer.customer_id
LIMIT 10
```

### S-074

レシート明細テーブル（receipt）の売上日（sales_ymd）に対し、当該週の月曜日からの経過日数を計算し、売上日、当該週の月曜日付とともに表示せよ。結果は10件表示させれば良い（なお、sales_ymdは数値でデータを保持している点に注意）。

```SQL
WITH t AS (
  SELECT
    sales_ymd,
    TO_DATE(CAST(sales_ymd AS TEXT), 'YYYYMMDD') AS sales_date,
    EXTRACT(DOW FROM TO_DATE(CAST(sales_ymd AS TEXT), 'YYYYMMDD')) - 1 AS days_from_monday
  FROM receipt
)
SELECT
  sales_ymd,
  CASE WHEN days_from_monday < 0 THEN 6 ELSE days_from_monday END AS days_from_monday,
  sales_date - INTERVAL '1 day' * (CASE WHEN days_from_monday < 0 THEN 6 ELSE days_from_monday END) AS last_monday
FROM t
LIMIT 10
```

### S-075

顧客テーブル（customer）からランダムに1%のデータを抽出し、先頭から10件データを抽出せよ。 

```SQL
SELECT * FROM customer WHERE RANDOM() < 0.01 LIMIT 10
```

### S-076

顧客テーブル（customer）から性別（gender_cd）の割合に基づきランダムに10%のデータを層化抽出し、性別ごとに件数を集計せよ。

```SQL
WITH t AS (
  (SELECT * FROM customer WHERE gender_cd = '0' AND RANDOM() < 0.1)
  UNION ALL
  (SELECT * FROM customer WHERE gender_cd = '1' AND RANDOM() < 0.1)
  UNION ALL
  (SELECT * FROM customer WHERE gender_cd = '9' AND RANDOM() < 0.1)
)
SELECT gender_cd, COUNT(1) FROM t GROUP BY gender_cd
```

### S-077

レシート明細テーブル（receipt）の売上金額（amount）を顧客単位に合計し、合計した売上金額の外れ値を抽出せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。なお、ここでは外れ値を平均から3σ以上離れたものとする。結果は10件表示させれば良い。

```SQL
WITH t AS (
  SELECT customer_id, SUM(amount) AS sum_amount
  FROM receipt
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
),
t2 AS (
  SELECT
    AVG(sum_amount) - STDDEV_SAMP(sum_amount) * 3 AS th_l,
    AVG(sum_amount) + STDDEV_SAMP(sum_amount) * 3 AS th_h
  FROM t
)
SELECT customer_id, sum_amount
FROM t
WHERE sum_amount <= (SELECT th_l FROM t2) OR (SELECT th_h FROM t2) <= sum_amount
LIMIT 10
```

### S-078

レシート明細テーブル（receipt）の売上金額（amount）を顧客単位に合計し、合計した売上金額の外れ値を抽出せよ。ただし、顧客IDが"Z"から始まるのものは非会員を表すため、除外して計算すること。なお、ここでは外れ値を第一四分位と第三四分位の差であるIQRを用いて、「第一四分位数-1.5×IQR」よりも下回るもの、または「第三四分位数+1.5×IQR」を超えるものとする。結果は10件表示させれば良い。

```SQL
WITH t AS (
  SELECT customer_id, SUM(amount) AS sum_amount
  FROM receipt
  WHERE NOT customer_id LIKE 'Z%'
  GROUP BY customer_id
),
t2 AS (
  SELECT q1 - (q3 - q1) * 1.5 AS th_l, q3 + (q3 - q1) * 1.5 AS th_h
  FROM (
    SELECT
      PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY sum_amount) AS q1,
      PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY sum_amount) AS q3
    FROM t
  ) t0
)
SELECT * FROM t WHERE sum_amount <= (SELECT th_l FROM t2) OR (SELECT th_h FROM t2) <= sum_amount LIMIT 10
```

### S-079

商品テーブル（product）の各項目に対し、欠損数を確認せよ。

```SQL
SELECT
  SUM(CAST(product_cd IS NULL AS INTEGER)) AS product_cd_null,
  SUM(CAST(category_major_cd IS NULL AS INTEGER)) AS category_major_cd_null,
  SUM(CAST(category_medium_cd IS NULL AS INTEGER)) AS category_medium_cd_null,
  SUM(CAST(category_small_cd IS NULL AS INTEGER)) AS category_small_cd_null,
  SUM(CAST(unit_price IS NULL AS INTEGER)) AS unit_price_null,
  SUM(CAST(unit_cost IS NULL AS INTEGER)) AS unit_cost_null
FROM product
```

### S-080

商品テーブル（product）のいずれかの項目に欠損が発生しているレコードを全て削除した新たなproduct_1を作成せよ。なお、削除前後の件数を表示させ、前設問で確認した件数だけ減少していることも確認すること。

```SQL
CREATE TABLE product_1 AS (
  SELECT * FROM product WHERE
  product_cd IS NOT NULL AND
  category_major_cd IS NOT NULL AND
  category_medium_cd IS NOT NULL AND
  category_small_cd IS NOT NULL AND
  unit_price IS NOT NULL AND
  unit_cost IS NOT NULL
)
```
```SQL
SELECT COUNT(1) FROM product;
```
```SQL
SELECT COUNT(1) FROM product_1;
```

### S-081

単価（unit_price）と原価（unit_cost）の欠損値について、それぞれの平均値で補完した新たなproduct_2を作成せよ。なお、平均値については1円未満を丸めること（四捨五入または偶数への丸めで良い）。補完実施後、各項目について欠損が生じていないことも確認すること。

```SQL
CREATE TABLE product_2 AS (
  WITH t AS (
    SELECT ROUND(AVG(unit_price)) AS avg_price, ROUND(AVG(unit_cost)) AS avg_cost
    FROM product
  )
  SELECT
    product_cd,
    category_major_cd,
    category_medium_cd,
    category_small_cd,
    COALESCE(unit_price, (SELECT avg_price FROM t)) AS unit_price,
    COALESCE(unit_cost, (SELECT avg_cost FROM t)) AS unit_cost
  FROM product
)
```
```SQL
SELECT
  SUM(CAST(product_cd IS NULL AS INTEGER)) AS product_cd_null,
  SUM(CAST(category_major_cd IS NULL AS INTEGER)) AS category_major_cd_null,
  SUM(CAST(category_medium_cd IS NULL AS INTEGER)) AS category_medium_cd_null,
  SUM(CAST(category_small_cd IS NULL AS INTEGER)) AS category_small_cd_null,
  SUM(CAST(unit_price IS NULL AS INTEGER)) AS unit_price_null,
  SUM(CAST(unit_cost IS NULL AS INTEGER)) AS unit_cost_null
FROM product_2
```

### S-082

単価（unit_price）と原価（unit_cost）の欠損値について、それぞれの中央値で補完した新たなproduct_3を作成せよ。なお、中央値については1円未満を丸めること（四捨五入または偶数への丸めで良い）。補完実施後、各項目について欠損が生じていないことも確認すること。

```SQL
CREATE TABLE product_3 AS (
  WITH t AS (
    SELECT
      ROUND(PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY unit_price)) AS med_price,
      ROUND(PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY unit_cost)) AS med_cost
    FROM product
  )
  SELECT
    product_cd,
    category_major_cd,
    category_medium_cd,
    category_small_cd,
    COALESCE(unit_price, (SELECT med_price FROM t)) AS unit_price,
    COALESCE(unit_cost, (SELECT med_cost FROM t)) AS unit_cost
  FROM product
)
```
```SQL
SELECT
  SUM(CAST(product_cd IS NULL AS INTEGER)) AS product_cd_null,
  SUM(CAST(category_major_cd IS NULL AS INTEGER)) AS category_major_cd_null,
  SUM(CAST(category_medium_cd IS NULL AS INTEGER)) AS category_medium_cd_null,
  SUM(CAST(category_small_cd IS NULL AS INTEGER)) AS category_small_cd_null,
  SUM(CAST(unit_price IS NULL AS INTEGER)) AS unit_price_null,
  SUM(CAST(unit_cost IS NULL AS INTEGER)) AS unit_cost_null
FROM product_3
```

### S-083

単価（unit_price）と原価（unit_cost）の欠損値について、各商品の小区分（category_small_cd）ごとに算出した中央値で補完した新たなproduct_4を作成せよ。なお、中央値については1円未満を丸めること（四捨五入または偶数への丸めで良い）。補完実施後、各項目について欠損が生じていないことも確認すること。

```SQL
CREATE TABLE product_4 AS (
  WITH t AS (
    SELECT
      category_small_cd,
      PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY unit_price) AS med_price,
      PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY unit_cost) AS med_cost
    FROM product
    GROUP BY category_small_cd
  )
  SELECT
    product_cd,
    category_major_cd,
    category_medium_cd,
    product.category_small_cd AS category_small_cd,
    COALESCE(unit_price, med_price) AS unit_price,
    COALESCE(unit_cost, med_cost) AS unit_cost
  FROM product
  INNER JOIN t
  ON product.category_small_cd = t.category_small_cd
)
```
```SQL
SELECT
  SUM(CAST(product_cd IS NULL AS INTEGER)) AS product_cd_null,
  SUM(CAST(category_major_cd IS NULL AS INTEGER)) AS category_major_cd_null,
  SUM(CAST(category_medium_cd IS NULL AS INTEGER)) AS category_medium_cd_null,
  SUM(CAST(category_small_cd IS NULL AS INTEGER)) AS category_small_cd_null,
  SUM(CAST(unit_price IS NULL AS INTEGER)) AS unit_price_null,
  SUM(CAST(unit_cost IS NULL AS INTEGER)) AS unit_cost_null
FROM product_4
```

### S-084

顧客テーブル（customer）の全顧客に対し、全期間の売上金額に占める2019年売上金額の割合を計算せよ。ただし、売上実績がない場合は0として扱うこと。そして計算した割合が0超のものを抽出せよ。 結果は10件表示させれば良い。

```SQL
WITH t AS (
  SELECT
    customer_id,
    SUM(CASE WHEN sales_ymd / 10000 = 2019 THEN CAST(amount AS FLOAT) ELSE 0 END) / SUM(amount) AS r2019
  FROM receipt
  GROUP BY customer_id
)
SELECT
  customer.customer_id,
  COALESCE(t.r2019, 0) AS r2019
FROM customer
LEFT JOIN t
ON customer.customer_id = t.customer_id
WHERE r2019 > 0
LIMIT 10
```

### S-085

顧客テーブル（customer）の全顧客に対し、郵便番号（postal_cd）を用いて経度緯度変換用テーブル（geocode）を紐付け、新たなcustomer_1を作成せよ。ただし、複数紐づく場合は経度（longitude）、緯度（latitude）それぞれ平均を算出すること。

```SQL
CREATE TABLE customer_1 AS (
  WITH t AS (
    SELECT postal_cd, AVG(latitude) AS avg_latitude, AVG(longitude) AS avg_longitude
    FROM geocode
    GROUP BY postal_cd
  )
  SELECT customer.*, t.avg_latitude, t.avg_longitude
  FROM customer
  LEFT JOIN t
  ON customer.postal_cd = t.postal_cd
)
```

### S-086

前設問で作成した緯度経度つき顧客テーブル（customer_1）に対し、申込み店舗コード（application_store_cd）をキーに店舗テーブル（store）と結合せよ。そして申込み店舗の緯度（latitude）・経度情報（longitude)と顧客の緯度・経度を用いて距離（km）を求め、顧客ID（customer_id）、顧客住所（address）、店舗住所（address）とともに表示せよ。計算式は簡易式で良いものとするが、その他精度の高い方式を利用したライブラリを利用してもかまわない。結果は10件表示すれば良い。

```SQL
SELECT
  customer_1.*,
  6371 * ACOS(
    SIN(PI() * customer_1.avg_latitude / 180) * SIN(PI() * store.latitude / 180) +
    COS(PI() * customer_1.avg_latitude / 180) * COS(PI() * store.latitude / 180) *
    COS(PI() * (customer_1.avg_longitude - store.longitude) / 180)
  ) AS distance
FROM customer_1
LEFT JOIN store
ON customer_1.application_store_cd = store.store_cd
LIMIT 10
```

### S-087

顧客テーブル（customer）では、異なる店舗での申込みなどにより同一顧客が複数登録されている。名前（customer_name）と郵便番号（postal_cd）が同じ顧客は同一顧客とみなし、1顧客1レコードとなるように名寄せした名寄顧客テーブル（customer_u）を作成せよ。ただし、同一顧客に対しては売上金額合計が最も高いものを残すものとし、売上金額合計が同一もしくは売上実績がない顧客については顧客ID（customer_id）の番号が小さいものを残すこととする。

```SQL
CREATE TABLE customer_u AS (
  WITH t2 AS (
    SELECT
      customer_name,
      postal_cd,
      customer.customer_id,
      RANK() OVER (PARTITION BY customer_name, postal_cd ORDER BY sum_amount DESC, customer.customer_id ASC) AS rnk
    FROM customer
    LEFT JOIN (
      SELECT customer_id, SUM(amount) AS sum_amount FROM receipt GROUP BY customer_id
    ) t
   ON customer.customer_id = t.customer_id
  )
  SELECT customer_name, postal_cd, customer_id
  FROM t2
  WHERE rnk = 1
)
```

### S-088

前設問で作成したデータを元に、顧客テーブルに統合名寄IDを付与したテーブル（customer_n）を作成せよ。ただし、統合名寄IDは以下の仕様で付与するものとする。

* 重複していない顧客：顧客ID（customer_id）を設定
* 重複している顧客：前設問で抽出したレコードの顧客IDを設定

```SQL
CREATE TABLE customer_n AS (
  SELECT
    customer.*,
    COALESCE(customer_u.customer_id, customer.customer_id) AS customer_id_u
  FROM customer
  LEFT JOIN customer_u
  ON customer.customer_name = customer_u.customer_name AND customer.postal_cd = customer_u.postal_cd
)
```

### S-089

売上実績がある顧客に対し、予測モデル構築のため学習用データとテスト用データに分割したい。それぞれ8:2の割合でランダムにデータを分割せよ。

```SQL
SELECT
  customer_id,
  SUM(amount) AS sum_amount,
  RANDOM() < 0.8 AS is_train
FROM receipt
GROUP BY customer_id
LIMIT 10
```

### S-090

レシート明細テーブル（receipt）は2017年1月1日〜2019年10月31日までのデータを有している。売上金額（amount）を月次で集計し、学習用に12ヶ月、テスト用に6ヶ月のモデル構築用データを3セット作成せよ。データの持ち方は自由とする。

```SQL
何を入力に何を出力するモデルを構築するか不明なため解答不能
```

### S-091

顧客テーブル（customer）の各顧客に対し、売上実績がある顧客数と売上実績がない顧客数が1:1となるようにアンダーサンプリングで抽出せよ。

```SQL
CREATE TABLE under_sampled_customer AS (

  WITH t AS (
    SELECT DISTINCT(customer_id) AS customer_id FROM receipt
  ),
  t2 AS (
    SELECT
      customer.customer_id AS customer_id,
      t.customer_id IS NOT NULL AS has_amount
    FROM customer
    LEFT JOIN t
    ON customer.customer_id = t.customer_id
  ),
  th AS (
    SELECT has_amount, COUNT(1) AS cnt FROM t2 GROUP BY has_amount
  ),
  c1 AS (
    SELECT customer_id, has_amount FROM t2 WHERE has_amount ORDER BY RANDOM() LIMIT (SELECT MIN(cnt) FROM th)
  ),
  c2 AS (
    SELECT customer_id, has_amount FROM t2 WHERE NOT has_amount ORDER BY RANDOM() LIMIT (SELECT MIN(cnt) FROM th)
  )

  SELECT * FROM c1
  UNION ALL
  SELECT * FROM c2
)
```

### S-092

顧客テーブル（customer）では、性別に関する情報が非正規化の状態で保持されている。これを第三正規化せよ。

```SQL
CREATE TABLE customer2 AS (
  SELECT customer_id, customer_name, gender_cd, birth_day, age, postal_cd, address, application_store_cd, application_date, status_cd
  FROM customer
);
CREATE TABLE gender AS (SELECT gender_cd, MAX(gender) AS gender FROM customer GROUP BY gender_cd);
```

### S-093

商品テーブル（product）では各カテゴリのコード値だけを保有し、カテゴリ名は保有していない。カテゴリテーブル（category）と組み合わせて非正規化し、カテゴリ名を保有した新たな商品テーブルを作成せよ。

```SQL
CREATE TABLE product2 AS (
  SELECT product.*, category_major_name, category_medium_name, category_small_name
  FROM product
  LEFT JOIN category
  ON product.category_major_cd = category.category_major_cd
    AND product.category_medium_cd = category.category_medium_cd
    AND product.category_small_cd = category.category_small_cd
)
```

### S-094

先に作成したカテゴリ名付き商品データを以下の仕様でファイル出力せよ。出力先のパスは"/tmp/data"を指定することでJupyterの"/work/data"と共有されるようになっている。なお、COPYコマンドの権限は付与済みである。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ有り
* 文字コードはUTF-8

```SQL
COPY product2 TO '/tmp/data/product2.csv' WITH CSV HEADER encoding 'UTF-8'
```

### S-095

先に作成したカテゴリ名付き商品データを以下の仕様でファイル出力せよ。出力先のパスは"/tmp/data"を指定することでJupyterの"/work/data"と共有されるようになっている。なお、COPYコマンドの権限は付与済みである。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ有り
* 文字コードはSJIS

```SQL
COPY product2 TO '/tmp/data/product2.csv' WITH CSV HEADER encoding 'SJIS'
```

### S-096

先に作成したカテゴリ名付き商品データを以下の仕様でファイル出力せよ。出力先のパスは"/tmp/data"を指定することでJupyterの"/work/data"と共有されるようになっている。なお、COPYコマンドの権限は付与済みである。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ無し
* 文字コードはUTF-8

```SQL
COPY product2 TO '/tmp/data/product2.csv' WITH CSV encoding 'UTF-8'
```

### S-097

先に作成した以下形式のファイルを読み込み、テーブルを作成せよ。また、先頭3件を表示させ、正しくとりまれていることを確認せよ。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ有り
* 文字コードはUTF-8

```SQL
-- 元テーブルの正確なスキーマを調べづらいため、元テーブルのコピーを作りデータを削除して使用する
CREATE TABLE product3 AS (SELECT * FROM product2);
TRUNCATE TABLE product3;
COPY product3 FROM '/tmp/data/product2.csv' WITH CSV HEADER encoding 'UTF-8'
```

### S-098

先に作成した以下形式のファイルを読み込み、テーブルを作成せよ。また、先頭3件を表示させ、正しくとりまれていることを確認せよ。

* ファイル形式はCSV（カンマ区切り）
* ヘッダ無し
* 文字コードはUTF-8

```SQL
-- 元テーブルの正確なスキーマを調べづらいため、元テーブルのコピーを作りデータを削除して使用する
CREATE TABLE product4 AS (SELECT * FROM product2);
TRUNCATE TABLE product4;
COPY product4 FROM '/tmp/data/product2.csv' WITH CSV encoding 'UTF-8'
```

### S-099

先に作成したカテゴリ名付き商品データを以下の仕様でファイル出力せよ。出力先のパスは"/tmp/data"を指定することでJupyterの"/work/data"と共有されるようになっている。なお、COPYコマンドの権限は付与済みである。

* ファイル形式はTSV（タブ区切り）
* ヘッダ有り
* 文字コードはUTF-8

```SQL
COPY product2 TO '/tmp/data/product2.csv' WITH CSV HEADER DELIMITER '\t' encoding 'UTF-8'
```

### S-100

先に作成した以下形式のファイルを読み込み、テーブルを作成せよ。また、先頭3件を表示させ、正しくとりまれていることを確認せよ。

* ファイル形式はTSV（タブ区切り）
* ヘッダ有り
* 文字コードはUTF-8

```SQL
-- 元テーブルの正確なスキーマを調べづらいため、元テーブルのコピーを作りデータを削除して使用する
CREATE TABLE product4 AS (SELECT * FROM product2);
TRUNCATE TABLE product4;
COPY product4 FROM '/tmp/data/product2.csv' WITH CSV HEADER DELIMITER '\t' encoding 'UTF-8'
```

