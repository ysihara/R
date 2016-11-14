# How to install or update R
「R」のインストールの方法やアップデート後の設定についてのメモ。

「R」はオープンソースでフリーの統計解析ソフトです。フリーとはいえ、世界中の研究者や開発者が、データを扱う上で便利な機能や新しいアルゴリズムを、「パッケージ」という形で日々追加しているので、「やりたい」と思うことはだいたい何でも出来てしまいます。

ここでは、「R」のインストールとその後の設定の仕方をまとめておきます。

<a id="index"></a>
<a href="#index"></a>
## 目次
* [Step1:「R」のダウンロードとインストール](#anchor1)
* [Step2: インストール後の設定](#anchor2)
* [Step3: 設定の確認](#anchor3)
* [オプション: 「RStudio」の設定](#anchor4)


<a id="anchor1"></a>
<a href="#anchor1"></a>  
## Step1:「R」のダウンロードとインストール
<!--ここに第1章の内容を書きます。-->
まず、Windows用のインストーラを[CRANのホームページ][]からダウンロードします。CRANのサイトにいき、中央パネル内上部の「<u>Download R for Windows</u>」をクリックします。

↓↓↓

いくつかサブディレクトリーが表示されますが、「<u>base</u>」をクリックします。

↓↓↓

上部パネル内の「<u>Download R x.x.x for Windows</u>」（x.x.xはバージョン名）をクリックし、最新版の「R」をダウンロードします。

↓↓↓

ダウンロードされたファイル「R-x.x.x-win.exe」をダブルクリックして、インストールを開始します。基本的には全てデフォルトのまま「OK」や「次へ」で大丈夫です（※64-bit版のWindowsを使っている場合は、途中に出てくるインストールする「R」のタイプを64-bit版にして下さい。）。

↓↓↓

インストール終了後、デスクトップにできた「R」のショートカットアイコンをダブルクリックし、無事に「R」が起動されたらインストール成功です。
<br />

<a id="anchor2"></a>
<a href="#anchor2"></a>
## Step2: インストール後の設定
<!--ここに第2章の内容を書きます。-->
インストールに成功したのを確認したら、Rが利用する環境変数の設定を行ないます。

##### 1. 設定ファイルのコピー＆ペースト
まず最初に、「R」をインストールしたディレクトリーの下にある「etc」フォルダの中にある Rcmd_environ, Rconsole, Rdevga, Rprofile.siteファイルをコピーし、自分の設定ファイルを置こうと思っている場所にペーストします。

私は「C:\Users\<ユーザー名>\AppData\Local」の下に「R」というディレクトリーを作成し、そこにペーストしました。

また、ライブラリー用に、このディレクトリーに「lib」というフォルダも作成しておきましょう。

##### 2. 設定ファイルのリネーム
ペーストした自分の設定ファイルを以下のようにリネームします。
* 「Rprofile.site」⇒「Rprofile」にリネーム
* 「Rcmd_environ」⇒「.Renviron.」にリネーム（※）

※「.」で始まるファイルを作成しようとする際、単純に先頭に「.Renviron」のみを入力するとエラーが出てしまいますが、末尾にも「.」を入れることによって、結果として「.Renviron」という名前のファイルを作成することができます。

##### 3. 環境変数「R_ENVIRON_USER」の設定
リネームが終わったら、OSの環境変数（※）「R_ENVIRON_USER」を作成し、「.Renviron」を参照するよう、「.Renviron」への絶対パスを値に入力します。(私の場合は、「C:\Users\<ユーザー名>\AppData\Local\R\.Renviron」としました。)

これにより、指定したディレクトリーにある「.Renviron」がRの起動時に使用されるようになります。

※環境変数の設定画面へは、「コンピュータ」＞「システムプロパティ」＞「システムの詳細設定」＞「詳細タブ」＞「環境変数」で行けます。画面下部のシステム環境変数ではなく、上部のユーザーの環境変数に上述のパスを追加します。

##### 4. 「.Renviron」の編集
下記のcodeを、「.Renviron」ファイルの先頭に追記します。ディレクトリへのパスは自分の環境に合わせて適宜修正してください。

```
# Rをインストールしたディレクトリー
R_HOME=C:/Program Files/R/R-x.x.x

# R_ENVIRON_USERに指定したディレクトリー
R_USER=C:/Users/<ユーザー名>/AppData/Local/R

R_LIBS=${R_USER}/lib
R_PROFILE_USER=${R_USER}/Rprofile
```

以上が一般的な設定となります。設定が終わったら、再度「R」を起動し、設定が反映されているか確認することをお勧めします。
<br />

<a id="anchor3"></a>
<a href="#anchor3"></a>
## Step3: 設定の確認
<!--ここに第3章の内容を書きます。-->
設定ができたら、デスクトップの「R」のショートカットアイコンをダブルクリックします。

下記のように、起動した「R」のコンソールに、
```
Sys.getenv("R_USER")
Sys.getenv("R_PROFILE_USER")
```
を入力すると、環境変数として使用されている値が確認できます。きちんと自分の設定が反映されていれば成功です。

以上で「R」のインストールおよび基本設定の完了です。お疲れ様でした。

「R」をアップデートする際も、ここに記載したものと同様の手順でアップデートおよびその後の設定ができます。

<a id="anchor4"></a>
<a href="#anchor4"></a>  
## オプション: 「RStudio」の設定
<!--ここに第4章の内容を書きます。-->

「RStudio」を使用している場合は、利用する「R」の設定を変更しておきましょう。

「RStudio」を起動＞「Tools」＞「Global Options...」＞「General」から、「R version:」および「Default working directory (when not in a project):」の「R」を最新のものに変更します。

「RStudio」を再起動し、設定が反映されているか確認して完了です。

### 参照リンク
* [CRANのホームページ][]
* [ぱーくん plus idea - フリーの統計解析環境「R」のインストールと設定][]

[CRANのホームページ]:	https://cran.r-project.org/	"CRANホームページ"
[ぱーくん plus idea - フリーの統計解析環境「R」のインストールと設定]:	http://web.plus-idea.net/2012/06/r-instal/	"ぱーくん plus idea"
