# setup-template-react

パッケージにReact+TypeScript-ESLint+WebPackの開発環境を展開します  
SCSSや画像などのリソースもデフォルトでバンドルするようになっています  
また、create-react-appと違って、設定ファイルは直接変更できるようになっています

## １．インストール方法

事前に npm -y init などでpackage.jsonは作っておいてください

```sh
npm -D i setup-template-react
```

インストールした時点で、追加コマンド無しでファイルが展開されます  
さらに既存のpackage.jsonの内容に、必要な情報を追加で書き込みます  

必要なパッケージの情報は書き込まれますが、この段階でインストールは行っていないので、以下のコマンドを一回実行してください

```sh
npm i
```

## ２．インストール後のディレクトリ構成

プログラムの作成はindex.tsxを書き換える形で行います

```txt
root/  
　├ dist/ (ファイル出力先)  
　└ front/ (フロントエンド用ディレクトリ)  
　　├ public/ (リソースHTMLファイル用)  
　　│　└ index.html  
　　├ src/ (JavaScript/TypeScript用ディレクトリ)  
　　│　├ .eslintrc.json  
　　│　├ index.tsx  
　　│　└ tsconfig.json  
　　└ webpack.config.js  
```

## ３．実行&ビルド

- ファイルを作成せずに実行確認  
npm start
- コンパイル結果をdistに出力  
npm run build
- コンパイル結果をdistに出力(監視状態)  
npm run watch
