# openjdkをインストール
 - https://jdk.java.net/ からアーカイブをダウンロードし任意のディレクトリに展開

   ※ バージョンは8以降ならどれでも良いです。(長期サポート版は廃止されたようなので...)
 - 環境変数JAVA_HOMEを設定
   ※ Oracle JREをインストールしている場合は、PATH環境変数を上書きされないよう注意
 - 確認
   コマンドプロンプトから以下のコマンドを実行し、インストールしたバージョンの情報が出力されることを確認
	java -version
 
# eclipseをインストール
 - https://www.eclipse.org/downloads/packages/ から Eclipse IDE for Enterprise Java and Web Developersをダウンロードし、任意のディレクトリに展開
 - eclipse.exeを実行

# tomcatのインストール
 - https://tomcat.apache.org/download-90.cgi から9.0系をダウンロードし任意のディレクトリに展開
 
   ※ Windowsインストーラは複数バージョンの併用に問題があるため、開発用にはzipアーカイブを使った手動インストールを推奨
 - bin\startup.batを実行し、サーバプロセスが起動すること、デフォルトページ(http://localhost:8080/)が表示されることを確認
 - (オプション) 管理UI(tomcat-manager)を有効化
   手順はgoogleで検索してください。

# Gitをインストール(オプション)
 - 基本機能はeclipseに組み込みのgitクライアントだけで使用できるので、お好みで。
   オリジナルgitのほか、github desktopも選択肢。

# eclipseの設定
 - JDKの設定
 
  メニュー>Window>Preference>Java>Installed JREにインストールしたopenjdkが設定されていることを確認(なければ追加)
 - mavenの設定
 
 メニュー>Window>Preference>Maven>User Settings
  ※ ローカルリポジトリには大量のファイルがコピーされるため、空き容量に余裕のあるドライブを指定
 - tomcatサーバの設定
 
 メニュー>Window>Preference>Server>Runtime Environments
  Add>リストからtomcat 9.0を選択>tomcatインストール先ディレクトリを指定
  メニュー>Window>Show View>Serversビューを開き、サーバを追加
  Serversビューからtomcatサーバの起動、停止ができることを確認

# リポジトリのセットアップ
 - メニュー>Show View>Git Repositoriesビューを開く
 - https://github.com/TsurumaiGO/IMANE をリモートリポジトリに追加
  (URLをクリップボードにコピーし、Git Repositoriesビューに貼り付け)
 - masterブランチをチェックアウト
 - ローカルリポジトリをeclipseプロジェクトとしてインポート
   Package Explorerビューにプロジェクト"workshop"が現れたらOK

# ビルド
 pom.xmlを選択>コンテキストメニュー>Run As > Maven install
 target配下にビルド済資材が出力される

# デバッグ
 - workshopプロジェクトを選択してコンテキストメニュー>Debug as>Debug on Server
 - 初回のみManually defina a new server>tomcat9.0 を新規作成
