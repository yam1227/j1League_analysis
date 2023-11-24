# J1リーグの試合結果を戦績とチーム間のゴール数、被ゴール数から予測する

## api_data
### form_another_game.ipynb
直近の戦績しか存在しないため、試合当時の戦績を最大５試合分取得する
### fixture_form.csv
試合ごと、各チームごとにその時点の戦績を登録したcsvファイル

## analytics
### glm_poisson.ipynb
**用いた手法**
1. ポアソン回帰より、チームごとに得点を予測
2. 予測した得点をもとに、各チームの得点確率を予測
3. チームごとの得点確率を独立と仮定して、同時確率を求める。

目的変数
* ホームチームの得点確率
* アウェイチームの得点確率

説明変数
* ホームチームの攻撃力（ホーム戦での得点数/アウェイチームのアウェイでの失点数）、ホームチームの直近の戦績、アウェイチームの直近の戦績
* アウェイチームの攻撃力（アウェイ戦での得点数/ホームチームのホームでの失点数）、ホームチームの直近の戦績、アウェイチームの直近の戦績

## api_get_code
[RapidAPI](https://rapidapi.com/hub)より、データを取得する際に用いたコード。
一部のみ反映

## scraping
[FootballLab](https://www.football-lab.jp/summary/team_style/j1/?year=2023)よりALL Styleの指数一覧のみ取得。  
各パラメータと、チーム名のリンクからhrefを取得し、その遷移先から、チームの英名を取得。

## 起動方法
1. [RapidAPI](https://rapidapi.com/hub)のアカウントを作成して、キーを取得する。
2. api_get_codeの配下のapi取得コード中のX-RapidAPI-Keyの要素部分xxxxを取得したキーに変更して、csv形式としてデータを取得する(gamedata_for_id.ipynb→team_statistics.ipynbの順で実装する)
3. api_data配下に新規のcsvファイルが作成されていることを確認する
4. form_another_game.ipynbを実装する
5. analytics配下のglm_poisson.ipynbを起動して結果を確認する
