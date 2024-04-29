# Aora

// appwrite のセッティング方法

app.json の ios と android に appwrite の id を記述する
$ "package": "com.jsm.aora"

プロジェクトのルートに lib フォルダを作成し、その中に appwrite.js ファイルを作成する。

そのファイルに
$ export const appwriteConfig = {
endpoint: "https://cloud.appwrite.io/v1",
platform: "com.jsm.aora",
projectId: "662f14ea00124dcbe203",
};
これを記述する.
platform にはバンドル ID
projectId にはプロジェクトの ID を記述する。

次にデータベースを作成する。
任意の名前を決定して、データベースの ID をコピーする。
その ID を appwrite.js に追記する。

続いて同ページの
createCollection ボタンからコレクションを作成する。
こちらも任意の名前をつけて ID をコピーし、appwrite.js に追記する。

collection は必要な文だけ作成し、
上記の手順で id を lib に追加する。

次にコレクションの属性を作成する。
collection 名を選択し、attributes
を選択。
create attribute ボタンから作成する。

例)String username 100
上記の例では string 型の
username を 100 文字以内の大きさで作成できる。
最後に required タブにチェックを入れて作成。
これも必要数だけ作成する。

次に setting タブから
Permissions で
Add a role to get started ボタンから Any をクリックし、
CRUD の役割にすべてチェックを入れる。

なお relationShip でデータベースのリレーションを設定可能。
このプロジェクトでは
user1 に対し、複数の video コレクションの属性が関わるので
video→user は
多対 1 となるため relation 欄では
Many to one を選択している。

On deletiong a document は null に設定する。

最後にもう一度 setting で
allUsers に対して、CRUD 操作ができるようにする。

最後にストレージの作成を行う。
storage タブから createBucket ボタンをクリックし、任意の名前をつけて作成し、id を libs に追記する。
setting から権限をすべてのユーザーに付与する。

//　認証
今回は ReactNative の SDKs を利用する。
ドキュメントから github のページに飛べるので、
$ npx expo install react-native-appwrite react-native-url-polyfill

このコマンドでインストールを行う。

github のドキュメントの指示に従って進める

初期リクエストを確認するための
コードを関数にして export させる。
それを submit ボタンなどの個人情報を送信する際に利用する場所で呼び出す。
(詳しくは appwrite.js と sign-up.jsx を確認。)

これで appwrite を用いたデータベース制作は完了。
