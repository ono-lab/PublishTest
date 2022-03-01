# 開発手引き

## git flow (ブランチ分け) について

- main: リリース前の完成したものを置いておくブランチ．原則このブランチでは開発しない．リポジトリ生成時にGitHubのSettings > Branchesの「Branch protection rules」でdevelopブランチからのPRによるマージしか行えないように設定する．
- develop: mainにマージする前の，各機能およびバグ修正を行ったものを集約するブランチ．featureブランチの分岐元およびマージ先となる．このブランチでも原則開発しない．
- feature/*: 各機能およびバグ修正を行うブランチ．原則このブランチで開発を行う．
- release: リリースブランチ．mainブランチが更新される度にこのブランチへのPRが作成される．作成されたPRがマージされれば，リリースのタグ付けおよびリリースノート，デプロイ（パッケージ化）が行われる．

## 開発の流れ

1. mainブランチを作成し，GitHubのSettings > Branchesの「Branch protection rules」でdevelopブランチからのPRによるマージしか行えないように設定する．
2. mainブランチを元にdevelopブランチを作成し，GitHubのSettings > Branchesの「Branch protection rules」でfeatureブランチからのPRによるマージしか行えないように設定する．
3. mainブランチを元にreleaseブランチを作成し，GitHubのSettings > Branchesの「Branch protection rules」でmainブランチからのPRによるマージしか行えないように設定する．
4. 開発をする場合は，feature/create_hogehogeやfeature/fix_hugahugaなどをdevelopブランチから分岐させて行う．
5. feature/create_hogehogeなど各featureブランチでの機能追加およびバグ修正が完成したらdevelopブランチへのPRを作成し，レビュアー全員の承認が得られればマージする．
6. ある程度の機能追加またはバグ修正が終わり，バージョン更新を行う場合はdevelopブランチからmainブランチへのPRを作成し，レビュアー全員の承認が得られればマージする．
7. mainブランチにマージされると，releaseブランチへのPRを作成するciが走る．レビュアー全員の承認が得られればマージする．
8. マージされれば，リリースのタグ付けおよびリリースノート，デプロイ（パッケージ化）を行うciが走る．

注意点
- マージされたブランチは原則mainとdevelop以外はマージ時に削除する．

現在mavenで行っている．設定ファイルの可読性やKotlinにも対応していることを考慮すると，将来的にはGradleに移行するのが良い．
- [GradleでのGitHub Packageのpublishの方法(GitHub公式から)](https://docs.github.com/en/actions/publishing-packages/publishing-java-packages-with-gradle#publishing-packages-to-github-packages)
- [Personal Access TokenのGradleにおける保管場所](https://medium.com/swlh/devops-with-github-part-1-github-packages-with-gradle-c4253cdf7ca6)

## バージョニングについて

vx.y.z  
x: メジャーバージョン．後方互換のない変更の場合に上げる．
y: マイナーバージョン．後方互換のある機能追加（enhancementタグに相当，ドキュメンテーション含む）の場合に上げる． 
z: パッチバージョン．後方互換のあるバグ修正（bugタグに相当）の場合に上げる．

- より詳しいバージョニングについては[こちら](https://semver.org/lang/ja/)