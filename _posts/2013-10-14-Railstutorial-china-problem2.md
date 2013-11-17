---
category: Rubyonrails
layout: post
title: Ruby On Rails中文教程问题2
time: 2013-10-14 12:30:00 -04:00
---

[Ruby On Rails教程](http://railstutorial-china.org/)目前看到第7章节，完成部分的代码已经上传[GitHub](https://github.com/wangyzyoga/sample_app)。继续把练习过程中遇到的问题进行整理，希望可以帮助遇到类似问题的人。

### 1. 重新设置BCrypt耗时因子

书中7.1.3章节中提到为测试环境重新设置BCrypt耗时因子：

    SampleApp::Application.configure do
      .
      .
      .
      # Speed up tests by lowering bcrypt's cost function.
      ActiveModel::SecurePassword.min_cost = true
    end

但我修改完成后，进行测试出现提示：

    undefined method `min_cost=' for ActiveModel::SecurePassword:Module
    (NoMethodError)

Google搜索设置BCrypt耗时因子方法，发现如下代码：

    require 'bcrypt'
    silence_warnings do
      BCrypt::Engine::DEFAULT_COST = BCrypt::Engine::MIN_COST
    end

按照上面方法修改完成后，再次进行测试就通过了。**暂时不知道原因，先通过再说～**

### 2. can't convert Symbol into string

书中7.3.1章节中提到处理存储失败的create动作：

    class UsersController < ApplicationController
      .
      .
      .
      def create
        @user = User.new(params[:user])    # Not the final implementation!
        if @user.save
          # Handle a successful save.
        else
          render 'new'
        end
      end
    end

修改完成后，进行测试出现提示：

    can't convert Symbol into string

问题出现原因是Gemfiles中缺少gem ‘strong_parameters’添加后，执行bundle install，再次进行测试就通过了。









    















