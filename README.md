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
echo "hello, world: 1行目" >> sample.txt
git add sample.txt
git commit -m 'commit task.1 途中'
```
# 2. タスク2の割り込み発生で、mainからタスク2のブランチを切り替え、コミット・プッシュをする
```
git switch main
git switch -c feature/02
echo "hello, world" > task2.txt
git add task2.txt
git commit -m 'commit task.2'
```
# 3. タスク1の作業に戻って作業を再開するが、ブランチを切り替え忘れている
```
echo "hello, world: 2行目" >> sample.txt
git add sample.txt
git commit -m 'commit task.1 完了'
```
### sample.txtを確認すると、ブランチを間違っていることを気づく
```
➜  case06 git:(main) ✗ cat sample.txt 
hello, world: 2行目
```

### コミットIDをメモする
```
git log
```
<img width="1435" alt="スクリーンショット 2021-05-15 3 22 57" src="https://user-images.githubusercontent.com/71377103/118313042-36a6f800-b52d-11eb-89c9-b5bebbcfb6c8.png">


# 2. 正しいブランチに切り替えて、コミットを付け替える

```
git switch -c feature/01
git cherry-pick <commit id>
```
### 正しいブランチに正しいコミットがあることを確認
```
git log
```
<img width="1435" alt="スクリーンショット 2021-05-15 3 24 12" src="https://user-images.githubusercontent.com/71377103/118313066-3d356f80-b52d-11eb-8690-b44dec45fffd.png">