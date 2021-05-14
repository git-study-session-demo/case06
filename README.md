# 特定のコミットだけを他のブランチにつけかえる

> 間違ったブランチにコミットしてしまったので正しいブランチにつけかえたい、特定のコミットだけmainブランチにマージしたいなんてことはありませんでしょうか？

# 0. リポジトリを作成しよう

### フォークする
<img width="1435" alt="スクリーンショット 2021-05-15 3 17 18" src="https://user-images.githubusercontent.com/71377103/118313001-2ee75380-b52d-11eb-89da-30b5b192f5da.png">

### クローンする
<img width="1435" alt="スクリーンショット 2021-05-15 3 16 32" src="https://user-images.githubusercontent.com/71377103/118312989-2abb3600-b52d-11eb-9f5a-42f5b736a3fa.png">

```
git clone <リポジトリURL>
```

# 1. 複数回コミットをする
```
git switch -c feature/01
```
```
echo "hello, world" > sample1.txt
```
```
git add .
```
```
git commit -m 'commit No.1'
```
```
echo "hello, world" > sample2.txt
```
```
git add .
```
```
git commit -m 'commit No.2'
```
```
echo "hello, world" > sample3.txt
```
```
git add .
```
```
git commit -m 'commit No.3'
```

### コミットIDをメモする
```
git log
```
<img width="1435" alt="スクリーンショット 2021-05-15 3 22 57" src="https://user-images.githubusercontent.com/71377103/118313042-36a6f800-b52d-11eb-89c9-b5bebbcfb6c8.png">


# 2. 別のブランチに"commit No.2"をマージする。

```
git switch main
```
```
git switch -c feature/02
```
```
git cherry-pick <commit id>
```
### "commit No.2"のコミットがあることを確認
```
git log
```
<img width="1435" alt="スクリーンショット 2021-05-15 3 24 12" src="https://user-images.githubusercontent.com/71377103/118313066-3d356f80-b52d-11eb-8690-b44dec45fffd.png">

