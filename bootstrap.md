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

####「new book」をクリックして、new.index.htmlを表示した状態にする

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
 }
```


#### app/views/books/index.html.erbに以下を記述
```
```


#### app/views/books/\_form.html.erbに以下を記述
```


```


#### app/views/books/\_form.html.erbに以下を記述
```
<%= form_for(book, html: {class: "form-horizontal"}) do |f|%>
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
    <%= f.label :title, class: "col-sm-2" %>
    <div class="col-sm-10">
      <%= f.text_field :title, class:"form-control" %>
    </div>
  </div>

  <div class="form-group">
    <%= f.label :memo, class: "col-sm-2" %>
    <div class="col-sm-10">
      <%= f.text_area :memo, class:"form-control"  %>
    </div>
  </div>

  <div class="form-group">
    <%= f.label :author, class: "col-sm-2" %>
    <div class="col-sm-10">
      <%= f.text_field :author, class:"form-control" %>
    </div>
  </div>

  <div class="form-group">
    <%= f.label :picture, class: "col-sm-2" %>
    <div class="col-sm-10">
      <%= image_tag(book.picture_url, size:'200x200') if book.picture.present? %>
      <%= f.file_field :picture %>
    </div>
  </div>

  <div class="actions">
    <%= f.submit class: "btn btn-default" %>
  </div>
<% end %>

```




#### app/views/layouts/application.html.erbに以下を記述
```

<body>
<div class="container">
  <div class="row">
    <div class="col-xs-10 col-xs-offset-1">
      <div class="col-xs-12">
        <h1>Books</h1>
        <%= link_to 'New Book', new_book_path, class: "btn btn-default "%>
      </div>
    </div>
  </div>
  <%= yield %>
</div>
</body>

```

#### app/views/books/index.html.erbに
以下を記述
```
<div class="row">
  <div class="col-xs-10 col-xs-offset-1">
    <p id="notice"><%= notice %></p>
    <% @books.each do |book| %>
      <div class="col-lg-4 col-sm-6 col-xs-12">
        <ul class="each_book">
          <li><%= image_tag book.picture , size: '100x100' %></li>
          <li>
            <ul class="data" >
              <li>Title:<%= book.title %></li>
              <li>Memo:<%= book.memo %></li>
              <li>Author:<%= book.author %></li>
            </ul>
          </li>
          <li>
            <ul class="buttons">
              <li><%= link_to 'Show', book, class: "btn btn-default btn-sm btn_black" %></li>
              <li><%= link_to 'Edit', edit_book_path(book), class: "btn btn-default btn-sm btn_black" %></li>
            </ul>
          <li><%= link_to 'Delete', book, method: :delete, data: { confirm: 'Are you sure?' }, class: "" %></li>
          </li>
        </ul>
      </div>
    <% end %>
  </div>
</div>
```


#### app/assets/stylesheets/application.cssに
以下を記述
```

body{
  margin: 0px;
  padding: 0px;
}

h1{
  margin: 10px 0px;
}

h2{
  margin: 30px 0px;
}

ul{
  list-style-type: none;
  margin: 0px;
  padding: 10px 0px;
 }

ul img{
  max-width: 100%;
  overflow: scroll;
  margin: 0px 0px 10px;
  padding: 0px;
  border: 1px solid #000;
}

ul{
  list-style-type: none;
  margin: 0px;
  padding: 10px 0px;
 }
```




#### app/views/layouts/new.html.erbに以下を記述
```
<div class="row">
  <div class="col-xs-10 col-xs-offset-1">
    <div class="col-xs-12">
      <h2>New Book</h2>
      <%= render 'form', book: @book %>
      <%= link_to 'Back', books_path, class: "btn btn-default btn-sm"  %>
    </div>
  </div>
</div>
```




#### app/views/layouts/edit.html.erbに#以下を記述
```
<div class="row">
  <div class="col-xs-10 col-xs-offset-1">
    <div class="col-xs-12">
      <h2>Editing Book</h2>
      <%= render 'form', book: @book %>
      <%= link_to 'Show', @book, class: "btn btn-default btn-sm" %>
      <%= link_to 'Back', books_path, class: "btn btn-default btn-sm" %>
    </div>
  </div>
</div>
```

#### app/views/layouts/show.html.erbに以下を記述
```
<div class="row">
  <div class="col-xs-8 col-xs-offset-2">
    <div class="col-xs-12">
      <p id="notice"><%= notice %></p>
      <ul>
        <li><%= image_tag(@book.picture_url, size:'300x300') if @book.picture.present? %></li>
        <li>Title:<%= @book.title %></li>
        <li>Memo:<%= @book.memo %></li>
        <li>Author:<%= @book.author %></li>
      </ul>
      <%= link_to 'Edit', edit_book_path(@book), class: "btn btn-default btn-sm" %>
      <%= link_to 'Back', books_path, class: "btn btn-default btn-sm" %>
    </div>
  </div>
</div>
```


#### app/assets/stylesheets/application.cssに以下を記述
```
  .btn_green{
    color: #fff;
    background-color: #2999af;
  }

  a.btn_green{
    color: #fff;
  }

  a.btn_green:visited{
    color: #fff;
  }
```


#### app/views/books/\_form.html.erbに以下を記述(submitにbtn_greenクラスを追加）
```
  <div class="actions">
    <%= f.submit class: "btn btn-default btn_green" %>
  </div>
```


#### app/views/layouts/application.html.erbに以下を記述(link_toにbtn_greenクラスを追加）
```
<%= link_to 'New Book', new_book_path, class: "btn btn-default btn_green"%>
```


#### app/assets/stylesheets/application.cssに以下を記述
```
a.btn_black{
  color: #fff;
  background-color: #000;
}

a.btn_black:hover{
  color: #fff;
  background-color: #ccc;
}


a.btn_black:visited{
  color: #fff;
  background-color: #000;
}
```


#### app/views/layouts/index.html.erbに以下を記述(showとeditのlink_toにbtn_blackを追加）
```
<li><%= link_to 'Show', book, class: "btn btn-default btn-sm btn_black" %></li>
<li><%= link_to 'Edit', edit_book_path(book), class: "btn btn-default btn-sm btn_black" %></li>
```

#### app/views/layouts/new.html.erbに以下を記述(backのlink_toにbtn_blackを追加）
```
<%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black"  %>
```


#### app/views/layouts/edit.html.erbに以下を記述(backとeditのlink_toにbtn_blackを追加）
```
      <%= link_to 'Show', @book, class: "btn btn-default btn-sm btn_black" %>
      <%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black" %>
```

## app/views/layouts/show.html.erbに以下を記述(backとeditのlink_toにbtn_blackを追加）
```
      <%= link_to 'Edit', edit_book_path(@book), class: "btn btn-default btn-sm btn_black" %>
      <%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black" %>
```



#### app/assets/stylesheets/application.cssに以下を記述
```
.detail li{
  padding: 0px 0px 10px 0px;
}
```


#### app/views/layouts/●.html.erbに以下を記述(detailクラスを追記）
```
<ul class="detail">
```


#### app/assets/stylesheets/application.cssに以下を記述
```
.each_book{
  height: 330px;
  margin: 15px 0px;
  padding: 20px;
  border: 2px solid #ccc;
  border-radius: 10px;
 }
```


#### app/views/layouts/●.html.erbに以下を記述(each_bookクラスを追加）
```
<% @books.each do |book| %>
      <div class="col-lg-4 col-sm-6 col-xs-12">
        <ul class="each_book">
```




#### app/assets/stylesheets/application.cssに以下を記述
```
.data{
  font-size:15px;
  height: 100px;
  overflow: scroll;
}

.data li{
  padding: 3px 0px;
}
```


#### app/views/layouts/index.html.erbに以下を記述dataクラスを追記
```
<ul class="data">
              <li>Title:<%= book.title %></li>
```


#### app/assets/stylesheets/application.cssに以下を記述
```
.buttons li{
  padding: 5px 5px 5px 0px;
  float:left;
 }

.buttons:after{
  content: "";
  display: block;
  clear: both;
 }
```


#### app/views/layouts/index.html.erbに以下を記述
```
<ul class="buttons">
              <li><%= link_to 'Show', book, class: "btn btn-default btn-sm btn_black" %></li>
```
