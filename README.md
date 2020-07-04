# 本テンプレートについて

EC2、RDSインスタンス、Auroraクラスターを定期的に停止、起動するLambda関数をデプロイするCloudFormationテンプレートです。指定したタグをインスタンスに設定することで、平日夜間、土日祝日にインスタンスを自動停止してくれます。

開発環境など利用料金をおさえたい環境にご利用ください。

## テンプレート適用手順

CloudFormationの画面から、「InstanceStartStop.yaml」をファイルアップロードしてデプロイすれば使用できます。下記パラメータを指定してください。

| パラメータ名 | デフォルト値 | 説明 |
| ------------- | ------------- | ------------- |
| StartSchedule | 0 21 ? * SUN-THU * | 起動時刻をcron形式で指定。UTC時刻なので注意。デフォルトは月－金の6:00 |
| StopSchedule | 0 15 ? * MON-FRI * | 停止時刻をcron形式で指定。UTC時刻なので注意。デフォルトは月－金の24:00 |
| TagKey | startstop | インスタンスに設定するタグのKey名を入力 |
| TagValue | True | インスタンスに設定するタグのValue(値)名を入力 |

## インスタンス設定手順

定期停止・起動を行いたいインスタンスにテンプレートで設定したタグ（デフォルトであればキー：startstop、値：True）を設定すればOKです。
EC2、RDSインスタンス、RDSクラスター（Aurora）に対応済み。


## 祝日の実行について

停止起動処理（Lamnda）の中で祝日判定を行っており、祝日であれば処理がスキップされるようになっている。祝日情報は下記から取得しています。
https://holidays-jp.github.io

