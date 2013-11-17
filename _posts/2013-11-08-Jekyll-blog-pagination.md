---
category: Rubyonrails
layout: post
title: 增加Jekyll博客分页功能
---

Jekyll博客分页功能添加步骤如下:

* _config.xml里面加上

      paginate:10  //每一页显示的文章数为10

* index.html里面加上:

      **分页输出**
      for post in paginator.posts
        content
      endfor
      
      **分页功能**
      if paginator.previous_page
        //判断输出前一个分页
        //"page" + paginator.previous_page
      endif
      if paginator.next_page
        //判断输出后一个分页
        //"page" + paginator.next_page
      endif
      for page in (1..paginator.total_pages)
        if page == paginator.page
          //如果是当前分页
          //page
        else
          //不是的话输出其他分页链接号码
          //"page" + page
        endif
      endfor
      
详细实现代码，可参见<https://github.com/wangyzyoga/wangyzyoga-blog/blob/gh-pages/index.html>


    















