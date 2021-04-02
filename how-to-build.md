# IMANE-PCビルド手順

## openjdkのインストール
 - https://jdk.java.net/ からアーカイブをダウンロードし任意のディレクトリに展開  
   ※ JDK8>JDK9以降で大きな非互換があり、今後に慣れるうえで9以降を推奨。
     本家openjdkでは長期サポート版は廃止されたが、別プロジェクト(AdoptOpenJDK：https://adoptopenjdk.net/)で長期サポート版がリリースされているJDK11が比較的安定か?
 - 環境変数JAVA_HOMEを設定  
   ※ Oracle JREをインストールしている場合は、PATH環境変数を上書きされないよう注意

 - 確認  
   コマンドプロンプトから以下のコマンドを実行し、インストールしたバージョンの情報が出力されることを確認  
	> java -version
 
## eclipseのインストール
 - https://www.eclipse.org/downloads/packages/ から Eclipse IDE for Enterprise Java and Web Developersをダウンロードし、任意のディレクトリに展開
 - [インストール先]\eclipse.iniをテキストエディタで開き、-vmオプションに[openjdkインストール先]\binを設定
 - eclipse.exeを実行

## tomcatのインストール
 - https://tomcat.apache.org/download-90.cgi から9.0系をダウンロードし任意のディレクトリに展開  
   ※ Windowsインストーラは複数バージョンの併用時に問題があるため、開発用にはアーカイブ形式を使った手動インストールを推奨
 - bin\startup.batを実行し、サーバプロセスが起動すること、デフォルトページ(http://localhost:8080/)が表示されることを確認
 - (オプション) 管理UI(tomcat-manager)を有効化  
   手順は割愛

## eclipseの設定
 - JDKの設定  
  メニュー > Window > Preference > Java > Installed JREにインストールしたopenjdkが設定されていることを確認(なければ追加)
 - mavenの設定
  - メニュー>Window > Preference > Maven > User Settings  
  ※ ローカルリポジトリには大量のファイルがコピーされるため、空き容量に余裕のあるドライブを指定
 - tomcatサーバの設定
  - メニュー>Window>Preference > Server > Runtime Environments
  - Add>サーバの一覧からtomcat 9.0を選択
   - Tomcat installed directory: >tomcatインストール先ディレクトリを指定
   - JRE: >先にインストールしたJDKを選択
  - メニュー>Window > Show View > Serversビューを開き、サーバを追加
  - Serversビューからtomcatサーバの起動、停止ができることを確認

  ※ eclipse本体、eclipseプロジェクト、tomcatのそれぞれに使用するJREを設定する項目があり、異なるJREが混在するとトラブルの原因になる。  
    最近のeclipseはJRE1.8を同梱するようになったため、設定不一致に要注意。

## リポジトリのセットアップ
 - eclipse>メニュー>Window>Show View>Git Repositoriesビューを開く
 - https://github.com/TsurumaiGO/IMANEのdevelブランチをリモートリポジトリに追加
   - 上記URLをクリップボードにコピーし、Git Repositoriesビューに貼り付け(Ctrl+V)>Clone Git Repositoryウィザードが開く
   - githubアカウントを使用する場合には、ウィザードの2ページ目で設定(参照のみの場合は匿名でOK)
   - Clone Git Repositoryウィザードの3ページ目(Local Destinationページ)で以下を指定;
     - Initial branch: develを選択
     - Imports all eclipse projects after clone finishesをチェック 
   - Package Explorerビューにプロジェクト"IMANE[IMANE devel]"が現れたらOK  

## プロジェクトのビルド
 - eclipse > IMANEプロジェクト > pom.xmlを選択 > コンテキストメニュー > Run As > Maven install
 - IMANEプロジェクト\target配下にビルド済資材が出力される

## プロジェクトのデバッグ
 - eclipse>workshopプロジェクト > コンテキストメニュー > Debug as > Debug on Server
  - 初回のみManually define a new server > tomcat9.0 を新規作成
 - Consoleビューに以下の行が出力されれば起動完了  
   INFO  [workshop]: 2021/04/02 07:57:33: started  
  
 
