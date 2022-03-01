# publish手順案

## 1つ目：完全自動化

1. `main`ブランチにプルリクエストでマージされると，ciによりリリース用のプルリクエストが作成される
2. `release/*`ブランチにプルリクエストでマージされると，ciにより以下が実行される
  -> これにより，パッケージ名とタグの対応付けが行われ，パッケージに対応するコードをタグから参照できる
	1. リリースタグ付け及びリリースノート生成
	2. リリースタグに対応したパッケージのpublish
3. onkのslackの`sip2`チャンネルに通知がいく

注意点

- `main`ブランチで開発しない -> GitHubのSettingsでmainの書き込み権限を制限する

## 2つ目：一部手動

1. リリース用のPRは手作業で作成
2. `release/*`ブランチにプルリクエストでマージされると，ciにより以下が実行される
  -> これにより，パッケージ名とタグの対応付けが行われ，パッケージに対応するコードをタグから参照できる
	1. リリースタグ付け及びリリースノート生成
	2. リリースタグに対応したパッケージのpublish
3. onkのslackの`sip2`チャンネルに通知がいく

## 3つ目：ほぼ手作業

1. `git tag -a ${tag} -m '${comment}'`でタグ付けし，pushする．ただし，`${tag}`はpom.xmlに記載したversionと一致させる必要がある．
2. vscodeでdeployする

## バージョンの意味
vx.y.z  
x: メジャーバージョン  
y: 機能追加（enhancementタグに相当，ドキュメンテーション含む）  
z: バグ修正（bugタグに相当）

## 参考
- [自動化手順](https://zenn.dev/itizawa/articles/b832c4e2a33661)
- [pom.xmlからのバージョンの取り方](https://stackoverflow.com/questions/63647949/getting-maven-project-version-within-github-actions)
