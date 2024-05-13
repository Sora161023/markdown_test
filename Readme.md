# バッテリー残量を常時表示
## はじめに
AIに頼りまくった超手抜きソフトです、99%AI製です
Java11.0.20.1で作成してます
> [!IMPORTANT]
> 実行に当たってJREのインストールが必須となります。JDKにJREは含まれるので、以下のサイトからJDKのインストールをあらかじめ行い、パスを通してください。  
>[Oracle JDK](https://www.oracle.com/java/technologies/downloads/ "Oracle Java Downloads")  
___
## 使い方
- そのまま実行するとシステムタスクトレイ内に表示されます。毎回起動するのも面倒なのでスタートアップ登録をお勧めします。
  - Battery.exeを任意のディレクトリに配置し、ショートカットを作成します。
  - Win + R を押し、以下のコマンドを打ちます。
    ```
    shell:startup
    ```
  - 先ほど作成したショートカットをこのフォルダに配置します。
- デフォルトだと非表示のシステムタスクトレイとして隠れてしまうので、タスクバー通知欄の ^ からアイコンをIMEの隣あたりまでD&Dします。これで次回実行時以降もタスクバーに常駐します。
- 色の変更 (v3.0以降の機能)
  - アイコンを右クリックしてSettingsを押すと、各バッテリ残量における色を変更することができます。
- ソフト終了時はアイコンをダブルクリックか、右クリックから終了を選択してください。
## コンパイル方法
自身で何か変更を行いたい場合はソースコードを変更した後コンパイルを行ってください。
以下にコンパイル例を表示します。
- javacでコンパイル  
    以下のコードを実行して.classを作成します。
    ```shell:Terminal
    javac --release11 -encoding utf-8 BatteryTrayApp.java
    ```
    日本語は使っていませんが文字コードはutf-8でないとコンパイルエラーになります。(開発時の文字コードかコメントが原因？)
- jarの作成  
    以下のコードを実行して.jarを作成します。
    ```shell:Terminal
    jar cvfe BatteryTrayApp.jar BatteryTrayApp BatteryTrayApp*.class
    ```
- jarからexeにコンパイル
  - Launch4jをインストール  
    以下のサイトからLaunch4jをインストールします。  
    [Install Launch4j](https://launch4j.sourceforge.net/ "Launch4j Home")  
  - Launch4jの設定等はググったほうがわかりやすいです。 
  - Restart the application after a crashはオフを推奨します。何かしらソフトにエラーがありうまく起動できない際、常に再実行され無駄に重くなるためです。
## 変更点
### 2024/05/12 v3.0
- 各バッテリー残量に応じて文字色を自由に設定できるように変更
  - バッテリー残量の方は固定、色はRGBで指定します。Saveを押すと同一ディレクトリ内にConfig.propertiesファイルが作成されます。  
> [!NOTE]
  デフォルトの色を使用したくなった場合や、色を変更した後アプリケーションがうまく起動しなくなった場合にはこのファイルを削除してください。デフォルト値に戻ります。  
- ~~アプリ同時起動数を1に制限~~
    ~~同時に起動できるアプリの数を1に制限しました。アプリが正しく終了し/なかった際にはLOCKファイルが残り、起動できなくなる可能性があります。%USERPROFILE%にBattery.LOCKが作成されているので、それを削除することで再び起動できるようになります。この機能は実験的に追加しています。~~
> [!NOTE]
    この機能は削除されました。
- 一部変数名の変更
___
### 2024/05/10 v2.2
- 描画の問題を修正
  - バッテリー残量が変化しないと電源接続状態が変化しても文字色が変わらなかった問題を修正
- 各種インターバル変更
  - 電源接続状態は5秒間隔、バッテリー残量取得は30秒間隔に変更
- デスクトップ環境などバッテリー非搭載モデル向けにキャンバスを作成
  - 利用できない環境ではキャンバスに"！"が表示されるようになりました。
- 一部変数名の統一化
___
### 2024/05/08 v2.1
- 描画の最適化
- バッテリー残量取得のインターバル変更
  - 10秒間隔に変更しました。
___
### 2024/05/08 v2.0
- バッテリー残量を7セグメント表記に変更
- バッテリー残量に応じて数値の色が変わるように変更

    | バッテリー状態 | 文字色 |
    |-------------:|:------:|
    | ~ 20%        |  橙色  |
    | ~ 50%        |  黄色  |
    | ~ 80%        |  白色  |
    | ~ 100%       |  緑色  |
    | 電源接続時    |  水色  |
- バッテリー残量取得のインターバル変更
  - 5秒間隔に変更(CPU使用率は0%なのでおそらく問題はない？というのも電源接続検知に60秒だと遅すぎるため)
- アイコンを追加
  - 以下のサイトから使用  
    [10,000 Free Icons SILHOUETTE ILLUST](https://www.silhouette-illust.com/illust/997 "SILHOUETTE ILLUST 997 BatteryIcon")  
___
### 2024/05/07 v1.0
- 初リリース
- バッテリー残量がタスクバーに表示されます。
