---
layout:     post
title:      ruby on rails 搭建twitter笔记
date:       2020-12-06
author:     HB
header-img:
catalog: true
tags:
    - Ruby on rails
---

# 6创建项目
$rails new lezhidaxue -d mysql

# 7配置项目
$mysql -u root -p
解决登录失败的情况：
https://stackoverflow.com/questions/39281594/error-1698-28000-access-denied-for-user-rootlocalhost

>CREATE DATABASE lezhidaxue_test;
> show databases;

>grant all privileges on lezhidaxue_development.* to dong@localhost identified by 'lezhidaxue';


>grant all privileges on lezhidaxue_test.* to dong@localhost identified by 'lezhidaxue';

>exit;

$rails db:schema:dump

# 8启动项目
$rails s

# 9生成controller和view

$rails generate controller demo index
```
rails generate controller NAME [action action] [options]
create  app/controllers/demo_controller.rb
       route  get 'demo/index'
      invoke  erb
      create    app/views/demo
      create    app/views/demo/index.html.erb
      invoke  test_unit
      create    test/controllers/demo_controller_test.rb
      invoke  helper
      create    app/helpers/demo_helper.rb
      invoke    test_unit
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/demo.coffee
      invoke    scss
      create      app/assets/stylesheets/demo.scss
```

# 10rails 如何响应请求
在public中新建demo/index.html,内容如下：
```ruby
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>This index is in public demo directory</h1>
</body>
</html>
```
刷新浏览器显示http://127.0.0.1:3000/demo/index显示

This index is in public demo directory

因为服务器会优先去public里边找路径请求，找不到再去controller里面找。相当于一个静态的网站。

# 11路由


# 12如何处理link
<%= link_to("index",{:controller => "demo",:action => "index"}) %>

<a href="/demo/index">index</a>

# 13处理带参数的链接
作用：

view中带参数的链接，然后controller捕捉到这个参数，向数据库中请求相应的内容，之后返回给view

<%= link_to("index with parameters",{:action => 'index', :spm => 'a7', :id => 55}) %>

http://127.0.0.1:3000/demo/index?id=55&spm=a7

demo_controller：
```Ruby
def index
	@spm = params[:spm]
	@id = params[:id]
end
index_view
id: <%= @id %>
spm: <%= @spm %>
```
# 14数据库介绍和常用命令

SHOW DATABASES;

CREATE DATABASES db_name;

USE db_name;

DROP DATABASE db_name;

# 15migration
用rails代替sql语句操作数据库的一个东西

操作数据库的指令

ruby写的


# 16生成migration

rails generate migration DoTestDemo

# 17生成用户模型



git checkout -b modeling-users #切换到另外一个分支



# 18生成model
rails g model User name:string email:string

rails -udong -p

use lezhidaxue_development;

show tables;

DESCRIBE users;

rails db:rollback



# 19 使用爬虫创建用户
rails console --sandbox


# 20 验证户名和电子邮件合法性

在db/migrate/***********_create_users.rb下

	 validates :name, presence: true

搜索 ruby on rails validation

rails db:migrate:运行所有尚未运行的迁移


rails console

dong = User.new(name:"",email:"liuyandong@gmail.com")

dong.save


select * from users;查看mysql 数据表中的内容


# 22写测试代码

require 'test_helper'

/test/model/user_test.rb:
``` ruby
class UserTest < ActiveSupport::TestCase
  # test "the truth" do
  #   assert true
  # end

  def setup
    @user = User.new(name: "luyanhui",email: "luyanhui@gmail.com")
  end

  test "the user model should be valid" do
    assert @user.valid?
  end

  test "the user model should be present" do
    @user.name = " "
    assert_not @user.valid?
  end

  test "the user name should not be longer than 20 characters" do
    @user.name = "a"*21
    assert_not @user.valid?
  end

  test "the email validation should accept valid address" do
    valid_addresses = %W[liuyndong@gmail.com meSSi@zhihu.com.cn R_cl@yahoo.cn]
    valid_addresses.each do |valid_address|
      @user.email = valid_address
      assert @user.valid?, "#{valid_address.inspect} should be valid"
    end
  end
  test "the email validation should inject invalid address" do
    invalid_addresses = %W[liuynd2onggmail.com me@n R_cl@...yahoo.cn]
    invalid_addresses.each do |invalid_address|
      @user.email = invalid_address
      assert_not @user.valid?, "#{invalid_address.inspect} should be invalid"
    end
  end
end


```
