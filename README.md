# setup-template-rails-react

既存のRailsプロジェクト上にReact+TypeScript-ESLint+WebPackの開発環境を展開します  
フロントエンドを完全にReactで構築し、RailsをAPIサーバとして利用する形の構造を作ります

## １．インストール方法

```sh
yarn --dev add setup-template-rails-react
```

インストールした時点で、追加コマンド無しでファイルが展開されます  
さらに既存のpackage.jsonの内容に、必要な情報を追加で書き込みます  

必要なパッケージの情報は書き込まれますが、この段階でインストールは行っていないので、以下のコマンドを一回実行してください

```sh
yarn install
```

## ２．インストール後のディレクトリ構成

プログラムの作成はindex.tsxを書き換える形で行います

```txt
root/  
　├ app/
　│　└ assets/
　│　　└ javascripts/ (トランスコンパイル出力ディレクトリ)
　│　　　├ bundle.js
　│　　　└ bundle.map
　└ front/ (フロントエンド用ディレクトリ)  
　　├ src/ (JavaScript/TypeScript用ディレクトリ)  
　　│　├ .eslintrc.json  
　　│　├ index.tsx  (サンプルReactソース)
　　│　└ tsconfig.json  
　　└ webpack.config.js  
```

## ３．Railsからの呼び出し方法

生成されるbundle.jsを読み込むために、以下の設定が必要となります

- /config/initializers/assets.rb に、以下の設定を追加  
(これを記述したらrailsを再起動)

```/config/initializers/assets.rb
Rails.application.config.assets.precompile += %w( bundle.js )
```

- /app/views 内のerbファイルに以下の内容を記述

```erb
<div id="root"></div>
<%= javascript_include_tag 'bundle.js' %>
```

## ４．Railsからの呼び出し方法の補足

- コントローラの作り方の例

以下のようにコマンドを入力してコントローラを作成する

```sh
rails generate controller root index
```

/app/views/root/index.html.erb の内容を直す

```/app/views/root/index.html.erb
<div id="root"></div>
<%= javascript_include_tag 'bundle.js' %>
```

/config/routes.rb の内容を修正する

```/config/routes.rb
Rails.application.routes.draw do
  root 'root#index'
end
```

## ５．実行&ビルド

- railsの起動  
npm start

- コンパイル結果を出力  
npm run build

- コンパイル結果を出力(監視状態)  
npm run watch
