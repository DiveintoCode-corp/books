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
    <ul>
      <li>
      <%= image_tag book.picture , size: '100x100' %></li>
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
      <ul>
        <li><%= image_tag book.picture , size: '100x100' %></li>
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
      <ul>
        <li><%= image_tag book.picture , size: '100x100' %></li>
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

### app/assets/stylesheets/application.css
### 以下を追記
```
ul{
  list-style-type: none;
  margin: 0px;
  padding: 10px 0px;
 }
```


## 3-1 Railsで作ったアプリに自分でcssをあてる


#### app/views/books/index.html.erb
#### ulにeach_bookクラスを追加
```
<ul class="each_book">
  <li><%= image_tag book.picture , size: '100x100' %></li>
  <li>Title:<%= book.title %></li>
  <li>Memo:<%= book.memo %></li>
  <li>Author:<%= book.author %></li>
  <li><%= link_to 'Show', book, class: "btn btn-default btn-sm" %></li>
  <li><%= link_to 'Edit', edit_book_path(book), class: "btn btn-default btn-sm"  %></li>
  <li><%= link_to 'Delete', book, method: :delete, data: { confirm: 'Are you sure?' }, class: "btn btn-default btn-sm" %></li>
</ul>
```


#### app/assets/stylesheets/aplication.css
```
.each_book{
  height: 330px;
  margin: 15px 0px;
  padding: 20px;
  border: 2px solid #ccc;
  border-radius: 10px;
 }
```

## 3-2 ulの入れ子

#### app/views/books/index.html.erb
#### ulを入れ子に
```
<ul class="each_book">
  <li><%= image_tag book.picture , size: '100x100' %></li>
  <li>
    <ul>
      <li>Title:<%= book.title %></li>
      <li>Memo:<%= book.memo %></li>
      <li>Author:<%= book.author %></li>
    </ul>
  </li>
  <li>
    <ul>
      <li><%= link_to 'Show', book, class: "btn btn-default btn-sm" %></li>
      <li><%= link_to 'Edit', edit_book_path(book), class: "btn btn-default btn-sm" %></li>
    </ul>
  <li><%= link_to 'Delete', book, method: :delete, data: { confirm: 'Are you sure?' }, class: "" %></li>
  </li>
</ul>

```

## 3-3 dateクラスとbuttonクラス
#### app/views/books/index.html.erb
#### data,buttonsクラスを適用

```
<ul class="each_book">
  <li><%= image_tag book.picture , size: '100x100' %></li>
  <li>
    <ul class="data">
      <li>Title:<%= book.title %></li>
      <li>Memo:<%= book.memo %></li>
      <li>Author:<%= book.author %></li>
    </ul>
  </li>
  <li>
    <ul class="buttons">
      <li><%= link_to 'Show', book, class: "btn btn-default btn-sm" %></li>
      <li><%= link_to 'Edit', edit_book_path(book), class: "btn btn-default btn-sm" %></li>
    </ul>
  <li><%= link_to 'Delete', book, method: :delete, data: { confirm: 'Are you sure?' }, class: "" %></li>
  </li>
</ul>

```

#### app/assets/stylesheets/aplication.css
```
.data{
  font-size:15px;
  height: 100px;
}
```

## 3-4 data li　の書き方

#### index.html.erb
```
.data li{
  padding: 3px 0px;
}

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

## 3-5 overflow:scroll
#### app/assets/stylesheets/aplication.css
```
.data{
  font-size:15px;
  height: 100px;
  overflow: scroll;
}
```

## 3-6 ul imgの書き方
## 3-7 max-width:100%
#### app/assets/stylesheets/aplication.css
```
ul img{
  max-width: 100%;
  margin: 0px 0px 10px;
  padding: 0px;
  border: 1px solid #000;
}
```

## 3-8 image_tagのsize
## レイアウトが崩れるので、相前後するがすでに2-6で適用されているもの対して解説


index.html.erb
```
<%= image_tag book.picture , size: '100x100' %>
```
#### show.html.erb
```
<%= image_tag(@book.picture_url, size:'300x300') if @book.picture.present? %>
```

## 3-9 a.btn_black:hoverの書き方
#### h1を追加
#### btn_breenクラスを追加
#### application.html.erb
```
<h1>Books</h1>
<%= link_to 'New Book', new_book_path, class: "btn btn-default btn_green" %>
```

#### btn_blackクラスを追加
#### new.html.erb
```
<%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black"  %>
```


#### btn_blackクラスを追加
#### edit.html.erb
```
<%= link_to 'Show', @book, class: "btn btn-default btn-sm btn_black" %> |
<%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black" %>

```

#### btn_greenクラスを追加
#### \_form.html.erb
```
<div class="actions">
  <%= f.submit class: "btn btn-default btn_green" %>
</div>
```

#### btn_blackクラスを適用
#### show.html.erb
```
<%= link_to 'Edit', edit_book_path(@book), class: "btn btn-default btn-sm btn_black" %>
<%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black" %>
```

#### app/assets/stylesheets/aplication.css
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

## 3-10 bodyにもmarginとpaddingを設定

#### app/assets/stylesheets/aplication.css
```
body{
  margin: 0px;
  padding: 0px;
}
```

## 3-11 col-sm-offset-1

#### application.html.erb
#### レスポンシブの入れ子

```
<div class="container">
  <div class="row">
    <div class="col-xs-10 col-xs-offset-1">
      <div class="col-xs-12">
        <h1>Books</h1>
        <%= link_to 'New Book', new_book_path, class: "btn btn-default btn_green" %>
      </div>
    </div>
  </div>

  <%= yield %>
</div>
```

### index.html.erb
### <% @books の直下でにdivタグを追加しレスポンシブ対応
　
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

#### レスポンシブの入れ子
#### edit.html.erb
```
<div class="row">
  <div class="col-xs-10 col-xs-offset-1">
    <div class="col-xs-12">
      <h2>Editing Book</h2>
      <%= render 'form', book: @book %>
      <%= link_to 'Show', @book, class: "btn btn-default btn-sm btn_black" %>
      <%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black" %>
    </div>
  </div>
</div>

```


#### レスポンシブの入れ子
#### new.html.erb
```
<div class="row">
  <div class="col-xs-10 col-xs-offset-1">
    <div class="col-xs-12">
      <h2>New Book</h2>
      <%= render 'form', book: @book %>
      <%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black"  %>
    </div>
  </div>
</div>

```

#### レスポンシブの入れ子
#### show.html.erb
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
      <%= link_to 'Edit', edit_book_path(@book), class: "btn btn-default btn-sm btn_black" %>
      <%= link_to 'Back', books_path, class: "btn btn-default btn-sm btn_black" %>
    </div>
  </div>
</div>

```

## 3-12 marginとpaddingで微調整
#### app/assets/stylesheets/aplication.css
```

h1{
  margin: 10px 0px;
}

h2{
  margin: 30px 0px;
}

a{
  color: #2999af;
}

a:visited{
  color: #2999af;
}

```
