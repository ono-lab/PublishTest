# 開発手引き

## git flow (ブランチ分け) について

- main: リリース前の完成したものを置いておくブランチ．原則このブランチでは開発しない．リポジトリ生成時にGitHubのSettings > Branchesの「Branch protection rules」でdevelopブランチからのPRによるマージしか行えないように設定する．
- develop: mainにマージする前の，各機能およびバグ修正を行ったものを集約するブランチ．featureブランチの分岐元およびマージ先となる．このブランチでも原則開発しない．
- feature/*: 各機能およびバグ修正を行うブランチ．原則このブランチで開発を行う．
- release/*: リリースブランチ．mainブランチが更新される度にこのブランチへのPRが作成される．作成されたPRがマージされれば，リリースのタグ付けおよびリリースノート，デプロイ（パッケージ化）が行われる．

## 開発の流れ

1. mainブランチを作成し，GitHubのSettings > Branchesの「Branch protection rules」でdevelopブランチからのPRによるマージしか行えないように設定する．
2. developブランチを作成し，GitHubのSettings > Branchesの「Branch protection rules」でfeatureブランチからのPRによるマージしか行えないように設定する．
3. 開発をする場合は，feature/create_hogehogeやfeature/fix_hugahugaなどをdevelopブランチから分岐させて行う．
4. feature/create_hogehogeなど各featureブランチでの機能追加およびバグ修正が完成したらdevelopブランチへのPRを作成し，レビュアー全員の承認が得られればマージする．
5. ある程度の機能追加またはバグ修正が終わり，バージョン更新を行う場合はdevelopブランチからmainブランチへのPRを作成し，レビュアー全員の承認が得られればマージする．
6. mainブランチにマージされると，releaseブランチへのPRを作成するciが走る．レビュアー全員の承認が得られればマージする．
7. マージされれば，リリースのタグ付けおよびリリースノート，デプロイ（パッケージ化）を行うciが走る．

注意点
- マージされたブランチは原則mainとdevelop以外はマージ時に削除する．