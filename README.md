# 01 Git / GitHub 基本操作

## レッスンのリポジトリ

- このレッスン: [git-lesson-01-basic](https://github.com/bp22029/git-lesson-01-basic.git)
- 次のレッスン: [git-lesson-02-gitflow](https://github.com/bp22029/git-lesson-02-gitflow.git)

## 学習目標

この演習では、Git / GitHub の始め方を2つ体験します。

- 方法A: GitHub から clone して始める方法
- 方法B: ローカルで作ったプログラムを `git init` して GitHub へ送る方法

終了後、次のことを説明できるようになることを目標にします。

- `git clone` で GitHub 上のリポジトリを PC に取得できる
- `git status` で作業状態を確認できる
- `git add` と `git commit` の役割を説明できる
- `git remote -v` で GitHub との接続先を確認できる
- `git push` で GitHub に変更を送れる
- `git init` でローカルフォルダを Git リポジトリにできる

## 重要な注意

方法Aと方法Bは、同じフォルダでは実行しません。

```text
方法A: GitHub から clone したフォルダで実行する
方法B: 新しく作った別フォルダで実行する
```

同じフォルダで両方を実行すると、remote 設定や commit 履歴が混ざり、初学者には原因を追いにくいエラーになります。

この授業では、方法Aを全員必須の基本演習として行います。方法Bも100分授業内で実施しますが、途中で詰まった場合は教員デモを見ながら流れを確認してもかまいません。

## 100分授業用の時間配分

| 時間 | 内容 | 目安 |
|---:|---|---|
| 0-10分 | Git / GitHub の役割説明 | ローカル、commit、GitHub の関係を確認する |
| 10-20分 | GitHub でテンプレートから自分用リポジトリを作成 | 方法Aの準備 |
| 20-55分 | 方法A: clone して編集、commit、push | 全員必須 |
| 55-65分 | 休憩またはトラブル対応 | 認証、clone 場所、保存忘れを確認 |
| 65-90分 | 方法B: ローカルから `git init` して GitHub へ push | 実習、難しい場合は教員デモ |
| 90-100分 | 方法Aと方法Bの違いを整理、作業記録を書く | 提出前確認 |

## 前提条件

- VS Code が使える
- Git がインストールされている
- GitHub アカウントがある
- GitHub にブラウザでログインできる
- ターミナルで `git --version` を実行できる

確認コマンド:

```bash
git --version
```

## このリポジトリで使うファイル

方法Aでは、次のファイルを使います。

```text
research_memo.md
data/observations.csv
```

`research_memo.md` は研究メモ、`data/observations.csv` は小さな観察データです。

方法Bでは、新しいフォルダに `HelloGit.java` を作ります。

## 授業用の作業場所を準備する

方法Aに入る前に、PC 上に授業用の親フォルダを1つ作ります。

フォルダ名の例:

```text
github-lesson-work
```

ターミナルで作る場合は、作業しやすい場所で次を実行します。

```bash
mkdir github-lesson-work
```

```bash
cd github-lesson-work
```

この親フォルダの中で各レッスンのリポジトリを clone します。`git clone` を実行すると、リポジトリ名と同じフォルダが自動で作成されます。

例:

```text
github-lesson-work/
├── student01-git-lesson-01-basic/
├── student01-git-lesson-02-gitflow/
├── git-lesson-03-conflict-group-a/
├── git-lesson-04-pr-review-group-a/
└── student01-git-lesson-05-actions-artifact/
```

確認ポイント:

- VS Code で `github-lesson-work` を開きます。
- `01`、`02` のようなフォルダを手動で作る必要はありません。
- clone 後は、clone で作成されたリポジトリフォルダの中に移動します。

## 作業の流れ

### 方法Aの流れ

```text
GitHub                         ローカルPC                      GitHub
+------------+   git clone    +-----------+   git push    +------------+
| repository | -------------> | commit    | ------------> | repository |
+------------+                +-----------+               +------------+
```

### 方法Bの流れ

```text
ローカルPC                                      GitHub
+-------------+   git init / commit / push    +----------------+
| HelloGit.java | --------------------------> | new repository |
+-------------+                              +----------------+
```

## 方法A: GitHub から clone して始める

方法Aは全員必須の基本演習です。GitHub 上にあるリポジトリを自分の PC に clone し、ファイルを編集して GitHub に push します。

### A-1. GitHub で自分用リポジトリを作成する

教員が指定したテンプレートリポジトリを開き、`Use this template` から自分用リポジトリを作成します。

確認ポイント:

- 自分の GitHub アカウント内にリポジトリが作成されたか確認します。
- リポジトリ画面に `research_memo.md` が表示されるか確認します。

### A-2. リポジトリの URL をコピーする

GitHub のリポジトリ画面で `Code` ボタンを押し、HTTPS の URL をコピーします。

URL の例:

```text
https://github.com/ユーザー名/リポジトリ名.git
```

### A-3. GitHub から clone する

授業用の親フォルダで実行します。`<GitHubリポジトリURL>` は自分のリポジトリの URL に置き換えます。

```bash
git clone <GitHubリポジトリURL>
```

確認ポイント:

- リポジトリ名と同じフォルダが作成されるか確認します。
- そのフォルダの中に `README.md` や `research_memo.md` があるか確認します。

### A-4. clone したフォルダに移動する

`<フォルダ名>` は clone で作成されたフォルダ名に置き換えます。

```bash
cd <フォルダ名>
```

確認ポイント:

- VS Code でこのフォルダを開きます。
- 方法Bでは、このフォルダを使いません。

### A-5. リポジトリの状態を確認する

```bash
git status
```

確認ポイント:

- `On branch main` と表示されるか確認します。
- `nothing to commit` と表示される場合、まだ変更はありません。
- エラーが出る場合は、ターミナルで開いている場所がリポジトリの中か確認します。

### A-6. VS Code で研究メモを編集する

VS Code で `research_memo.md` を開き、次の項目に自分の内容を追記します。

```text
- 今日の作業:
- 気づいたこと:
```

保存を忘れないでください。

### A-7. 変更されたファイルを確認する

```bash
git status
```

確認ポイント:

- `modified: research_memo.md` が表示されるか確認します。
- 赤色で表示される場合、まだ commit の準備はできていません。

### A-8. 変更内容を commit の対象にする

```bash
git add research_memo.md
```

```bash
git status
```

確認ポイント:

- `research_memo.md` が緑色で表示されるか確認します。
- 緑色で表示されれば commit の準備ができています。

### A-9. commit する

```bash
git commit -m "研究メモを更新"
```

確認ポイント:

- `1 file changed` のような表示が出るか確認します。
- commit メッセージは、日本語でも英語でもかまいません。

### A-10. GitHub との接続先を確認する

```bash
git remote -v
```

確認ポイント:

- `origin` という名前で GitHub の URL が表示されるか確認します。
- `fetch` と `push` の2行が表示されます。

例:

```text
origin  https://github.com/ユーザー名/リポジトリ名.git (fetch)
origin  https://github.com/ユーザー名/リポジトリ名.git (push)
```

### A-11. GitHub に push する

```bash
git push
```

確認ポイント:

- エラーが出なければ、GitHub に変更が送られています。
- GitHub のリポジトリ画面を再読み込みし、`research_memo.md` が更新されているか確認します。

### 補足: `git push origin main` の意味

`git push` は、現在のブランチを設定済みの送信先に送るコマンドです。

より明示的に書くと、次のように実行できます。

```bash
git push origin main
```

意味:

- `origin`: GitHub 上の接続先につけた名前
- `main`: GitHub に送るブランチ名

つまり、`git push origin main` は「ローカルの `main` ブランチを、`origin` という名前の GitHub リポジトリへ送る」という意味です。

## 演習課題A: 研究メモを自分の内容に更新する

ここからは、方法Aの説明付き基本手順を参考にして、自分で小さな変更を作ります。

課題:

- `research_memo.md` に、自分の研究テーマに近い観察メモを2行以上追加する
- `data/observations.csv` は読むだけにし、今回は変更しない
- 変更後、`git add`、`git commit`、`git push` の流れを自分で実行する

追加する内容の例:

```text
- 今日の作業: 実験条件AとBの違いを確認した。
- 気づいたこと: 測定値を見る前に、記録方法をそろえる必要がある。
```

実行するコマンドの例:

```bash
git status
```

```bash
git add research_memo.md
```

```bash
git commit -m "研究テーマに関するメモを追加"
```

```bash
git push
```

この課題の主目的:

- ファイル編集そのものではなく、変更を Git で記録して GitHub に送る流れを体感すること

## 方法B: ローカルで作ったプログラムを GitHub へ送る

方法Bでは、先にローカル PC で新しいフォルダとプログラムを作り、その後で GitHub に空のリポジトリを作成して push します。

詰まった場合は、無理に進めず教員デモで流れを確認してください。方法Aができていれば、この授業の基本目標は達成しています。

### B-1. 方法Aとは別の場所に移動する

方法Aで clone したフォルダの中では実行しません。授業用の作業場所に戻ってから始めます。

例:

```bash
cd ..
```

確認ポイント:

- `research_memo.md` があるフォルダの中ではないことを確認します。
- 不安な場合は、教員に現在の場所を見せてください。

現在の場所を確認するコマンド:

```bash
pwd
```

PowerShell では次も使えます。

```powershell
Get-Location
```

### B-2. 新しいフォルダを作る

```bash
mkdir hello-git
```

```bash
cd hello-git
```

確認ポイント:

- 方法Aの clone フォルダとは別の `hello-git` フォルダにいることを確認します。

### B-3. `HelloGit.java` を作る

VS Code で `HelloGit.java` を作成し、次の内容を書いて保存します。

```java
public class HelloGit {
    public static void main(String[] args) {
        System.out.println("Hello, Git and GitHub!");
    }
}
```

必要に応じて、Java をコンパイルして実行します。

```bash
javac HelloGit.java
```

```bash
java HelloGit
```

確認ポイント:

- ターミナルに `Hello, Git and GitHub!` と表示されるか確認します。
- Java が実行できない場合でも、`HelloGit.java` を作成して commit する演習は続けられます。
- `HelloGit.class` が作成された場合でも、今回は `git add` しません。

### B-4. Git リポジトリとして初期化する

```bash
git init
```

確認ポイント:

- `Initialized empty Git repository` のような表示が出るか確認します。
- この時点で、`hello-git` フォルダが Git で管理されるようになります。

### B-5. 状態を確認する

```bash
git status
```

確認ポイント:

- `HelloGit.java` が未追跡ファイルとして表示されるか確認します。
- `HelloGit.class` が表示された場合でも、今回は追加しません。
- まだ commit の対象にはなっていません。

### B-6. `HelloGit.java` を commit の対象にする

```bash
git add HelloGit.java
```

```bash
git status
```

確認ポイント:

- `HelloGit.java` が緑色で表示されるか確認します。

### B-7. commit する

```bash
git commit -m "helloプログラムを追加"
```

確認ポイント:

- `1 file changed` のような表示が出るか確認します。

### B-8. GitHub 上で空のリポジトリを作成する

GitHub の画面で新しいリポジトリを作成します。

リポジトリ名の例:

```text
hello-git
```

重要:

GitHub 上で次の項目は追加しません。

- README
- `.gitignore`
- license

理由:

ローカルにはすでに commit があるため、GitHub 側にも最初から README などを追加すると、履歴がずれて `failed to push some refs` の原因になることがあります。

### B-9. ブランチ名を main にする

```bash
git branch -M main
```

確認ポイント:

- エラーが出なければ、現在のブランチ名が `main` になります。

### B-10. GitHub リポジトリを remote として登録する

`<GitHubリポジトリURL>` は、B-8 で作成した空リポジトリの HTTPS URL に置き換えます。

```bash
git remote add origin <GitHubリポジトリURL>
```

### B-11. remote を確認する

```bash
git remote -v
```

確認ポイント:

- `origin` として GitHub の URL が表示されるか確認します。
- `fetch` と `push` の2行が表示されるか確認します。

### B-12. GitHub に push する

```bash
git push -u origin main
```

確認ポイント:

- GitHub のリポジトリ画面を再読み込みします。
- `HelloGit.java` が GitHub 上に表示されるか確認します。

## 演習課題B: ローカルで作った Java ファイルを GitHub に送る

課題:

- 方法Aとは別の `hello-git` フォルダで作業する
- `HelloGit.java` を自分で作成する
- commit メッセージを自分で考えて commit する
- GitHub 上に空のリポジトリを作り、`git remote add origin ...` と `git push -u origin main` で送る

余裕がある場合:

`HelloGit.java` の表示を、自分の研究テーマに近い短い文に変更して2つ目の commit を作ります。

例:

```java
System.out.println("I will record small research changes with Git.");
```

確認する Git の流れ:

```text
新しいフォルダを作る
  -> ファイルを作る
  -> git init
  -> git add
  -> git commit
  -> GitHub に空リポジトリを作る
  -> git remote add origin ...
  -> git push -u origin main
```

補足:

`-u` は、今後の `git push` や `git pull` で使う標準の送信先を記録するための指定です。次回以降は、同じブランチであれば次のように短く実行できます。

```bash
git push
```

## 方法Aと方法Bの違い

| 項目 | 方法A: clone して始める | 方法B: git init して始める |
|---|---|---|
| 最初にあるもの | GitHub 上のリポジトリ | ローカル PC 上の新しいフォルダ |
| 最初に使う主なコマンド | `git clone` | `git init` |
| remote の設定 | clone 時に自動で `origin` が設定される | `git remote add origin ...` で自分で設定する |
| GitHub リポジトリ | 先に作成する | 後から空で作成する |
| README など | テンプレートに含まれている | GitHub 側では追加しない |
| 授業での位置づけ | 全員必須の基本演習 | 追加演習、詰まった場合は教員デモで補う |
| よくあるつまずき | clone 場所、認証、保存忘れ | 同じフォルダで実行、空でない GitHub リポジトリへの push |

## 期待される結果

方法A:

- `research_memo.md` に自分の作業メモが追加されている
- `git remote -v` で `origin` が確認できる
- GitHub 上でも `research_memo.md` の変更内容が確認できる

方法B:

- 新しい `hello-git` フォルダで `HelloGit.java` を作成している
- `git init`、`git add`、`git commit` を実行している
- GitHub 上の空リポジトリに `HelloGit.java` を push できている

## よくあるエラー

### `fatal: not a git repository`

原因:

ターミナルで開いている場所が Git リポジトリではありません。

確認すること:

```bash
pwd
```

PowerShell では次も使えます。

```powershell
Get-Location
```

対応:

- 方法Aでは、clone したフォルダの中に移動します。
- 方法Bでは、`git init` を実行したフォルダの中に移動します。

### `nothing to commit`

原因:

ファイルを保存していない、または変更がすでに commit 済みです。

確認すること:

- VS Code でファイルを保存したか
- `git status` で変更が表示されるか

### `Authentication failed`

原因:

GitHub への認証が完了していません。

確認すること:

- GitHub にログインしているか
- HTTPS で clone した場合、Git Credential Manager の画面で認証したか
- 教員の指示に従って認証をやり直してください

### `remote origin already exists`

原因:

すでに `origin` という remote が登録されています。

確認すること:

```bash
git remote -v
```

対応:

- 方法Aでは、clone した時点で `origin` が自動設定されているため、`git remote add origin ...` は実行しません。
- 方法Bでこのエラーが出た場合、同じフォルダで以前に remote を登録している可能性があります。教員に確認してから対応してください。

### `failed to push some refs`

原因の例:

- GitHub 側に README、`.gitignore`、license などを追加してから push しようとした
- 自分のローカル履歴と GitHub 側の履歴がずれている
- 別のブランチに push しようとしている

確認すること:

```bash
git remote -v
```

```bash
git status
```

対応:

- 方法Bでは、GitHub 上で空のリポジトリを作ったか確認します。
- 授業中は無理に複雑な解決をせず、教員に画面を見せてください。

## 提出物

方法A:

- GitHub 上の自分用リポジトリ URL
- `research_memo.md` を更新した commit の URL
- 授業中の作業記録

方法B:

- `HelloGit.java` を push した GitHub リポジトリ URL
- `helloプログラムを追加` commit の URL
- 方法Bで詰まった場合は、どこで詰まったかを書いた作業記録

## 振り返り質問

- 方法Aと方法Bでは、最初にあるリポジトリはどこにありますか。
- `git clone` と `git init` は何が違いますか。
- `git remote -v` では何を確認できますか。
- `git add` と `git commit` は何が違いますか。
- `git push origin main` の `origin` と `main` は、それぞれ何を表していますか。

## 提出前チェックリスト

方法A:

- [ ] GitHub から clone した
- [ ] clone したフォルダに移動した
- [ ] `git status` で作業状態を確認した
- [ ] `research_memo.md` を編集した
- [ ] `git add research_memo.md` を実行した
- [ ] `git commit -m "研究メモを更新"` を実行した
- [ ] `git remote -v` で `origin` を確認した
- [ ] `git push` を実行した
- [ ] GitHub 上で変更を確認した

方法B:

- [ ] 方法Aとは別のフォルダで作業した
- [ ] 新しい `hello-git` フォルダを作った
- [ ] `HelloGit.java` を作った
- [ ] `git init` を実行した
- [ ] `git status` を確認した
- [ ] `git add HelloGit.java` を実行した
- [ ] `git commit -m "helloプログラムを追加"` を実行した
- [ ] GitHub 上で空のリポジトリを作成した
- [ ] GitHub 上で README、`.gitignore`、license を追加しなかった
- [ ] `git branch -M main` を実行した
- [ ] `git remote add origin <GitHubリポジトリURL>` を実行した
- [ ] `git remote -v` を確認した
- [ ] `git push -u origin main` を実行した
- [ ] 作業記録を書いた
