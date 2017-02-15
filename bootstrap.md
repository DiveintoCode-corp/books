
##1-1 Bootstrapとは
##1-2 BootstrapをRailsで使うには
##1-3 Bootstrapのgem

```
git init
git clone　https://github.com/igaiga/books_app_rails_5001
cd workspace/igaiga/books_app_rails_5001
```

###workspaceが無い場合、

```
mkdir workspace
```

###Gemfileに以下を記述
```
gem 'twitter-bootstrap-rails'

bundle install
```

###cssファイルをアプリのディレクトリに配置

```
rails generate bootstrap:install static
```

##サーバー起動

```
rails s
```

##「new book」から4つほどテストデータを投稿
