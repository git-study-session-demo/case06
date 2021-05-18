# 特定のコミットだけを他のブランチにつけかえる

> 間違ったブランチにコミットしてしまったので正しいブランチにつけかえたい、特定のコミットだけmainブランチにマージしたいなんてことはありませんでしょうか？  
今回は複数のタスクを割り込みでやるとき、間違ったブランチにコミットしてしまった時のシナリオをハンズオンでやります。

# 0. リポジトリを作成しよう

### フォークする
<img width="1435" alt="スクリーンショット 2021-05-15 3 17 18" src="https://user-images.githubusercontent.com/71377103/118313001-2ee75380-b52d-11eb-89da-30b5b192f5da.png">

### クローンする
<img width="1435" alt="スクリーンショット 2021-05-15 3 16 32" src="https://user-images.githubusercontent.com/71377103/118312989-2abb3600-b52d-11eb-9f5a-42f5b736a3fa.png">

```
git clone <リポジトリURL>
```

# 1. タスク1のブランチをきり、途中までコミットをする
```
git switch -c feature/01
echo "task1: file 1" > task1_01.txt
git add task1_01.txt
git commit -m 'commit task.1 途中'
```
# 2. タスク2の割り込み発生で、mainからタスク2のブランチを切り替え、コミット・プッシュをする
```
git switch main
git switch -c feature/02
echo "task2" > task2.txt
git add task2.txt
git commit -m 'commit task.2'
```
# 3. タスク1の作業に戻って作業を再開するが、ブランチを切り替え忘れている
```
echo "task1: file 2" > task1_02.txt
git add task1_02.txt
git commit -m 'commit task.1 完了'
```
### lsでファイル一覧を確認すると、ブランチを間違っていることを気づく
```
➜  case06 git:(feature/02) ls
README.md    task1_02.txt task2.txt
```

### コミットIDをメモする
```
git log
```
<img width="951" alt="スクリーンショット 2021-05-18 14 10 56" src="https://user-images.githubusercontent.com/869103/118594836-00939d80-b7e5-11eb-984a-d297f68aea70.png">


# 2. 正しいブランチに切り替えて、コミットを付け替える

```
git switch feature/01
git cherry-pick <commit id>
```
### 正しいブランチに正しいコミットがあることを確認
```
git log
```
<img width="1068" alt="スクリーンショット 2021-05-18 14 34 50" src="https://user-images.githubusercontent.com/869103/118595935-4bfa7b80-b7e6-11eb-8ee8-24c3de5fbcaf.png">
