rmtr - Redmine Timelog Recorder
====


概要
----

rmtrは、Redmineのチケットに対する作業時間の記録をコマンドラインから行うためのRubyスクリプトです。


インストール
----

まず、実行に必要なgemパッケージをインストールします。

    $ gem install -y mechanize

次に`rmtr`をパスの通った所に置いて実行権限を与えます。

    $ cp rmtr ~/bin/rmtr
    $ chmod +x ~/bin/rmtr

最後に`rmtr.yml.example`を`~/.rmtr.yml`にコピーして、内容を変更します。

    $ cp rmtr.yml.example ~/.rmtr.yml


設定
----

接続するRedmineのURL、ログイン情報および活動については、`~/.rmtr.yml`に記述します。

    redmine:
      base_url: https://redmine.serverworks.co.jp:9001
      username: ogura@serverworks.co.jp
      password: oirapyov
      activities:
        - { id: 1, key: c, label: コーディング }
        - { id: 2, key: t, label: テスト }

活動(activities)は、接続するRedmineの経過時間ページ(http://example.com/timelog/edit?issue_id=xxx)
にアクセスし、活動のSELECT要素の内容を参考に設定してください。


実行方法
----

引数を省略して実行するとヘルプが表示されます。

    $ ./rmtr
    rmt - Redmine Timelog Recorder
    
      Usage:
        ./rmtr -a <活動> -i <チケットID> -t [時間] [-cd]
    
      Options:
        -a value, --activity=value        活動
                                          c  コーディング
                                          t  テスト
        -c value, --comment=value         コメント
        -d YYYY-MM-DD, --date=YYYY-MM-DD  日付
        -i id, --issue=id                 チケットID
        -t n, --hours=n                   時間
    
      Example:
        ./rmtr -i 10000 -a c -t 3
          チケット#10000に3時間のコーディングを記録
        ./rmtr -i 10000 -a t -t 0.5 -c 'テストをしました'
          チケット#10000に0.5時間のテストをコメントつきで記録

最低限必要なオプションは、`-a`と`-i`と`-t`の3つです。

時間の記録に成功すると、以下のように表示されます。

    $ ./rmtr -i 7653 -a o -t 0.3
    ============================================================
    チケット #7653
    ------------------------------------------------------------
    時間    : 0.3
    作業    : その他
    ============================================================
    作業時間を記録しました。

適宜、エイリアスを定義してご活用ください。


ライセンス
----

rmtrのライセンスは[MIT license](http://creativecommons.org/licenses/MIT/)です。
