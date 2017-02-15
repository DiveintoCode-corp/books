#Bootstrap,CSS手順

## 1-1 Bootstrapとは
## 1-2 BootstrapをRailsで使うには
## 1-3 Bootstrapのgem

```
git init
git clone　https://github.com/igaiga/books_app_rails_5001
cd workspace/igaiga/books_app_rails_5001
```

#### workspaceが無い場合
```
mkdir workspace
```

#### Gemfileに以下を記述
```
gem 'twitter-bootstrap-rails'
```

```
bundle install
```

#### cssファイルをアプリのディレクトリに配置

```
rails generate bootstrap:install static
```

#### サーバー起動

```
rails s
```

####「new book」から4つほどテストデータを投稿

## 2-1 Bootstrapのクラスをあててみる
## 2-2 form-group

####「new book」をクリックして、new.html.erbを表示した状態にする

#### app/views/books/\_form.html.erbに以下を記述
#### divタグのfieldクラスをform-groupクラスに変更
#### 見た目の変化はわずか（各要素の間に若干余白が生まれる）

```
<%= form_for(book) do |f| %>
  <% if book.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(book.errors.count, "error") %> prohibited this book from being saved:</h2>

      <ul>
      <% book.errors.full_messages.each do |message| %>
        <li><%= message %></li>
      <% end %>
      </ul>
    </div>
  <% end %>

  <div class="form-group">
    <%= f.label :title %>
    <%= f.text_field :title %>
  </div>

  <div class="form-group">
    <%= f.label :memo %>
    <%= f.text_area :memo %>
  </div>

  <div class="form-group">
    <%= f.label :author %><br>
    <%= f.text_field :author %>
  </div>

  <div class="form-group">
    <%= f.label :picture %><br>
    <%= f.file_field :picture %>
  </div>

  <div class="actions">
    <%= f.submit %>
  </div>
<% end %>
```

## 2-3 Railsのタグにクラスをあてる
## 2-4 form-control

#### app/views/books/\_form.html.erbに以下を記述
#### f.text_field,t.text_areaタグにform-controlクラスを適用
#### 入力欄が横に広がり、角が丸くなる

```
<%= form_for(book) do |f| %>
  <% if book.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(book.errors.count, "error") %> prohibited this book from being saved:</h2>

      <ul>
      <% book.errors.full_messages.each do |message| %>
        <li><%= message %></li>
      <% end %>
      </ul>
    </div>
  <% end %>

  <div class="form-group">
    <%= f.label :title %>
    <%= f.text_field :title, class:"form-control"  %>
  </div>

  <div class="form-group">
    <%= f.label :memo %>
    <%= f.text_area :memo, class:"form-control"  %>
  </div>

  <div class="form-group">
    <%= f.label :author %><br>
    <%= f.text_field :author, class:"form-control"  %>
  </div>

  <div class="form-group">
    <%= f.label :picture %><br>
    <%= f.file_field :picture %>
  </div>

  <div class="actions">
    <%= f.submit %>
  </div>
<% end %>
```

## 2-5link_toのclass:にbtn

## h1をh2タグに変更
## app/views/books/new.html.erbに以下を記述
## btnクラスを適用
## backのリンクに余白が生まれる
```
<h2>New Book</h2>
<%= render 'form', book: @book %>
<%= link_to 'Back', books_path, class:"btn" %>
```


## 2-6 複数のBootstrapクラスをあてる(btn-sm btn-default
#### app/views/books/new.html.erbに以下を記述
#### btn btn-defaultをlink_toに記述

```
<h2>New Book</h2>
<%= render 'form', book: @book %>
<%= link_to 'Back', books_path, class: "btn btn-default" %>

```

#### app/views/books/\_form.html.erbに以下を記述
#### btn btn-defaultを追加
```
<div class="actions">
  <%= f.submit class: "btn btn-default" %>
</div>
```


## h1をh2タグに変更
#### app/views/books/edit.html.erbに以下を記述
#### btn btn-default btn-smを追加
```
<h1>Editing Book</h1>
<%= render 'form', book: @book %>
<%= link_to 'Show', @book, class: "btn btn-default btn-sm" %> |
<%= link_to 'Back', books_path, class: "btn btn-default btn-sm"  %>

```


#### app/views/books/show.html.erbに以下を記述
#### pタグをulに変更
#### image_tagに変更し、300x300のサイズを適用

```
<p id="notice"><%= notice %></p>
<ul class="detail">
  <li><%= image_tag(@book.picture_url, size:'300x300') if @book.picture.present? %></li>
  <li>Title:<%= @book.title %></li>
  <li>Memo:<%= @book.memo %></li>
  <li>Author:<%= @book.author %></li>
</ul>
<%= link_to 'Edit', edit_book_path(@book) %>
<%= link_to 'Back', books_path %>
```

#### app/views/books/show.html.erbに以下を記述
#### btn-default btn-smを適用

```
<p id="notice"><%= notice %></p>
<ul class="detail">
  <li><%= image_tag(@book.picture_url, size:'300x300') if @book.picture.present? %></li>
  <li>Title:<%= @book.title %></li>
  <li>Memo:<%= @book.memo %></li>
  <li>Author:<%= @book.author %></li>
</ul>
<%= link_to 'Edit', edit_book_path(@book), class: "btn btn-default btn-sm" %>
<%= link_to 'Back', books_path, class: "btn btn-default btn-sm" %>

```

#### app/views/books/index.html.erbに以下を適用
#### btn btn-default btn-smを適用

```
<li><%= link_to 'Show', book, class: "btn btn-default btn-sm" %></li>
<li><%= link_to 'Edit', edit_book_path(book), class: "btn btn-default btn-sm"  %></li>
<li><%= link_to 'Delete', book, method: :delete, data: { confirm: 'Are you sure?' }, class: "btn btn-default btn-sm" %></li>

```

## 2-7 画面の段組の概念
## 2-8 グリッドシステム
## 2-9 containerとrow

####「back」をクリックして、index.html.erbに移動
#### app/views/books/index.html.erbに以下を記述
#### テーブルレイアウトになっているので、まず、ulを使ったレイアウトに変更
#### <%= book.picture %>をimage_tagに変更

```
<p id="notice"><%= notice %></p>
<% @books.each do |book| %>
    <%= image_tag book.picture , size: '100x100' %>
    <ul>
      <li>Title:<%= book.title %></li>
      <li>Memo:<%= book.memo %></li>
      <li>Author:<%= book.author %></li>
      <li><%= link_to 'Show', book %></li>
      <li><%= link_to 'Edit', edit_book_path(book) %></li>
      <li><%= link_to 'Delete', book, method: :delete, data: { confirm: 'Are you sure?' }%></li>
    </ul>
<% end %>
<%= link_to 'New Book', new_book_path %>
```


## 2-9 containerとrow

#### app/views/layout/application.html.erbに以下を記述
#### divタグを追加し、containerクラスをあてる
#### yieldの説明はRailsコースで済んでいない場合は解説
```
  <body>
    <div class="container">
      <%= yield %>
    </div>
  </body>
```


## app/views/books/index.html.erbに以下を記述
## 新たにdivタグを作り、rowを記述
## これでcontainerとrowが入れ子に

```
<div class="row">
  <p id="notice"><%= notice %></p>
  <% @books.each do |book| %>
      <%= image_tag book.picture , size: '100x100' %>
      <ul>
        <li>Title:<%= book.title %></li>
        <li>Memo:<%= book.memo %></li>
        <li>Author:<%= book.author %></li>
        <li><%= link_to 'Show', book %></li>
        <li><%= link_to 'Edit', edit_book_path(book) %></li>          <li><%= link_to 'Delete', book, method: :delete, data: { confirm: 'Are you sure?' }%></li>
      </ul>
 <% end %>
 <%= link_to 'New Book', new_book_path %>
</div>
```


## 2-10 col-lg-4の意味
#### app/views/books/index.html.erbに以下を記述
#### 新たにdivタグを作り、col-lg-4 col-sm-6 col-xs-12を追記
#### col-lg-4 col-sm-6 col-xs-12を適用したdivタグは必ずeachの下の階層に置く
#### 各divタグが横並びになる

```
<div class="row">
  <p id="notice"><%= notice %></p>
  <% @books.each do |book| %>
    <div class="col-lg-4 col-sm-6 col-xs-12">
      <%= image_tag book.picture , size: '100x100' %>
      <ul>
        <li>Title:<%= book.title %></li>
        <li>Memo:<%= book.memo %></li>
        <li>Author:<%= book.author %></li>
        <li><%= link_to 'Show', book %></li>
        <li><%= link_to 'Edit', edit_book_path(book) %></li>          <li><%= link_to 'Delete', book, method: :delete, data: { confirm: 'Are you sure?' }%></li>
      </ul>
   </div>
 <% end %>
  <%= link_to 'New Book', new_book_path %>
</div>
```


## 2-11段組とmargin,padding

#### app/assets/stylesheets/application.cssに以下を追記
#### ulの前の余計な余白がなくなる
```
ul{
  margin: 0px;
  padding: 10px 0px;
 }s
```

### app/views/books/index.html.erb以下のコードを切り取る
```
<%= link_to 'New Book', new_book_path %>
```

### app/views/layout/application.rbに切り取ったものを貼り付けし、btn btn-defaultを適用

```
<div class="container">
  <%= link_to 'New Book', new_book_path, class: "btn btn-default" %>
  <%= yield %>
</div>
```

## 3-1
