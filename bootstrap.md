Bootstrap,CSS


##1-1 Bootstrapとは
##1-2 BootstrapをRailsで使うには
##1-3 Bootstrapのgem

git init
git clone　https://github.com/igaiga/books_app_rails_5001
cd workspace/igaiga/books_app_rails_5001

#workspaceが無い場合、
mkdir workspace

#Gemfileに以下を記述
gem 'twitter-bootstrap-rails'

bundle install

#cssファイルをアプリのディレクトリに配置
rails generate bootstrap:install static

#サーバー起動
rails s

#「new book」から4つほどテストデータを投稿

##2-1 Bootstrapのクラスをあててみる
##2-2 form-group

#「new book」をクリックして、new.index.htmlを表示した状態にする

#app/views/books/_form.html.erbに以下を記述
#divタグのfieldクラスをform-groupクラスに変更
#見た目の変化はわずか（各要素の間に若干余白が生まれる）

——————————————————————————————————————————————————————
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
——————————————————————————————————————————————————————


##2-3 Railsのタグにクラスをあてる
##2-4 form-control

#app/views/books/_form.html.erbに以下を記述
#f.text_field,t.text_areaタグにform-controlクラスを適用
#入力欄が横に広がり、角が丸くなる
——————————————————————————————————————————————————————
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
——————————————————————————————————————————————————————


##2-5link_toのclass:にbtn

#h1をh2タグに変更
#app/views/books/new.html.erbに以下を記述
#btnクラスを適用
#backのリンクに余白が生まれる
——————————————————————————————————————————————————————
<h2>New Book</h2>

<%= render 'form', book: @book %>

<%= link_to 'Back', books_path, class:"btn" %>
——————————————————————————————————————————————————————


#2-6 複数のBootstrapクラスをあてる(btn-sm btn-default
#app/views/books/new.html.erbに以下を記述
#btn btn-defaultをlink_toに記述

——————————————————————————————————————————————————————
<h2>New Book</h2>
<%= render 'form', book: @book %>
<%= link_to 'Back', books_path, class: "btn btn-default" %>

——————————————————————————————————————————————————————
