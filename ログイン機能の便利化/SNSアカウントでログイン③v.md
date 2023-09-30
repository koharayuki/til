## ユーザー管理機能を実装

※ミニアプリを使用して実装を進めます。

### 新規アプリケーションを作成する

【ターミナル】
```
% rails _7.0.0_ new mini_sns -d mysql
% cd mini_sns
```

### データベースを作成する

【config/database.yml】
```
default: &default
 adapter: mysql2
 # encoding: utf8mb4
 encoding: utf8
 pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
 username: root
  password:
  socket: /tmp/mysql.sock
```

【ターミナル】
```
% rails db:create
```

### コントローラーを作成して、ルーティングを編集する

【ターミナル】
```
% rails g controller users
```

今回は、indexとnewのみを使用します。

【config/routes.rb】
```ruby
Rails.application.routes.draw do
 root 'users#index'  
 resources :users, only: :new  
end
```

### deviseをインストールする

ログイン機能を実装するために、 deviseをGemfileに記述します。

【Gemfile】
```
#中略
gem 'devise'
```

【ターミナル】
```
% bundle install
```

### devise関連のコマンドを実行する

以下のコマンドを順に実行します。

- deviseの設定ファイルをRailsアプリケーションにインストールするコマンド
- Userモデルの作成コマンド
- deviseのビューをインストールするコマンド

【ターミナル】
```
% rails g devise:install
% rails g devise user
% rails g devise:views
```

### マイグレーションファイルを編集する

ニックネーム、苗字、名前、誕生日カラムを追加します。

【db/migrate/XXXXXXXXXXXXXXXX_devise_create_users.rb】
```ruby
class DeviseCreateUsers < ActiveRecord::Migration[7.0]
 def change
   create_table :users do |t|
     t.string :nickname, null: false
     t.string :lastname, null: false
     t.string :firstname, null: false
     t.date   :birthday, null: false
     ## Database authenticatable
     t.string :email,              null: false, default: ""
     t.string :encrypted_password, null: false, default: ""

     ## Recoverable
     t.string   :reset_password_token
     t.datetime :reset_password_sent_at
     t.datetime :remember_created_at
     t.timestamps null: false
   end

   add_index :users, :email,                unique: true
   add_index :users, :reset_password_token, unique: true
   # add_index :users, :confirmation_token,   unique: true
   # add_index :users, :unlock_token,         unique: true
 end
end
```

【ターミナル】
```
% rails db:migrate
```

usersテーブルが以下のようになっていれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/b64f2449-edaa-4f73-ad15-1f690826bc8b)

### ビューファイルを編集する

追加したカラムに対応する、フォームを追加します。

【app/views/devise/registrations/new.html.erb】
```erb
<h2>Sign up</h2>

<%= form_for(resource, as: resource_name, url: registration_path(resource_name)) do |f| %>
 <%= render "devise/shared/error_messages", resource: resource %>

 <div class="field">
   <%= f.label :nickname %><br />
   <%= f.text_field :nickname, autofocus: true %>
 </div>

 <div class="field">
   <%= f.label :lastname %><br />
   <%= f.text_field :lastname %>
 </div>

 <div class="field">
   <%= f.label :firstname %><br />
   <%= f.text_field :firstname %>
 </div>

 <div class="field">
   <%= f.label :birthday %><br />
   <%= f.date_select :birthday, start_year: 1950, end_year: 2019 %>
 </div>

 <div class="field">
   <%= f.label :email %><br />
   <%= f.email_field :email, autofocus: true, autocomplete: "email" %>
 </div>

   <div class="field">
     <%= f.label :password %>
     <% if @minimum_password_length %>
     <em>(<%= @minimum_password_length %> characters minimum)</em>
     <% end %><br />
     <%= f.password_field :password, autocomplete: "new-password" %>
   </div>

   <div class="field">
     <%= f.label :password_confirmation %><br />
     <%= f.password_field :password_confirmation, autocomplete: "new-password" %>
   </div>

 <div class="actions">
   <%= f.submit "Sign up" %>
 </div>
<% end %>

<%= render "devise/shared/links" %>
```

次に、トップページの作成と編集を行います。

<img width="542" alt="スクリーンショット 2023-09-26 11 23 39" src="https://github.com/koharayuki/til/assets/132040884/9af406a7-0df6-435c-a6bc-3ee67ccdabf8">

表示する画面は、以下の条件で場合分けします。

| 条件	               | 表示する画面               |
| ------------------ | ----------------------- |
| ログインしている場合	   | ユーザー名とログアウトボタン    |
| ログインしていない場合	 | ログインと新規登録のリンク     |

【app/views/users/index.html.erb】
```erb
<% if user_signed_in? %>
  <li><%= "#{current_user.nickname}でログイン中" %></li>
  <li><%= link_to 'ログアウト', destroy_user_session_path, method: :delete %></li>
<% else %>
  <p>ログインしていません</p>
  <li><%= link_to 'ログイン', new_user_session_path %></li>
  <li><%= link_to '新規登録', new_user_path %></li>
<% end %>
```

トップページで「新規登録」を選択した場合のビューを作成と編集します。

「new.html.erb」を作成します。

<img width="737" alt="スクリーンショット 2023-09-30 14 42 00" src="https://github.com/koharayuki/til/assets/132040884/b92f6f0d-c3ac-4964-a253-8f1b4ed73fc6">

【app/views/users/new.html.erb】
```erb
<%= link_to "メールアドレスで登録", new_user_registration_path%>
```










