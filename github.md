# githubの使い方

準備
- `git init`: ローカルリポジトリ作成
- `git remote add <remote> <URL>`: リモートの追加
- `git remote rm <remote>`: リモートの削除
- `git remote -v`: リモートの確認

リモートリポジトリに変更を反映させる
- `git add <file1> <file2>` : コミットするファイルを置いておく（インデックスに登録）
- `git commit -m "message"`: ローカルリポジトリにコミット
- `git push <remote> <branch>`: リモートにプッシュ

リモートリポジトリから変更を取得する
- `git fetch <remote>` : リモートから変更を取得（リモート追跡ブランチ）
- `git merge <remote>/<branch>`: リモート追跡ブランチをローカルブランチにマージ
- `git pull <remote> <branch>`: fetchとmergeをいっぺんに行う

リモートリポジトリをローカルにダウンロード
（カレントディレクトリにリモートリポジトリの名前のファルダが作成される）
- `git clone <URL>` : リモートリポジトリを自分のコンピュータにクローン

-----

githubから持ってくるとき
```
cd gitfolder
git init
git remote add origin URL # リモート名デフォルトはorigin
git pull origin main
```
githubへ持っていくとき
```
cd gitfolder
git init
git remote add origin URL
git add <file1> <file2>
git add <file3>
git commit -m "commut message"
git push origin main
```



-----

gitバージョン確認

```
git --version
```

ユーザー名とメアドの登録
（その時のレポジトリのみで使用する場合は`--global`を除く）

```
git config --global user.name "ユーザー名"
git config --global user.email "メールアドレス"
```

その他

```
git status # 変更したファイル名を表示
git diff # 変更内容を表示
git log # コミット履歴
```
