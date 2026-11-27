---
layout: post
title: "巧用 Laravel-admin 的 Grid::init () 方法"
date: 2019-12-10 11:41:14 +0800
categories: laravel php
---

在使用 Laravel-admin 的日常开发中，经常需要编写资源排序及后台用户操作权限等问题，在每个 Controller 里写相同的代码显得非常冗余，有没有好的办法把这些代码抽离出来呢？

当然有啦！

在 `app/Admin/bootstrap.php` 文件中添加以下代码即可：

```php
<?php

use Encore\Admin\Grid;
use Encore\Admin\Facades\Admin;

Encore\Admin\Form::forget(['map', 'editor']);

Grid::init(function (Grid $grid) {
    // 排序
    $order_ignore_models = [];
    if (!in_array(get_class($grid->model()->eloquent()), $order_ignore_models)) {
        $grid->model()->orderBy('id', 'desc');
    }

    // 权限
    $permissions = [
        'index',
        'view',
        'create',
        'edit',
        'delete',
    ];
    $user_permissions = [];
    foreach ($permissions as $permission) {
        // 这里的权限名称要事先约定好，为 `table-name.permission`
        $user_permissions[$permission] = str_replace('_', '-', $grid->model()->getTable()) . '.' . $permission;
    }

    if (Admin::user()->cannot($user_permissions['create'])) {
        $grid->disableCreateButton();
    }
    $grid->actions(function (Grid\Displayers\Actions $actions) use ($user_permissions) {
        if (Admin::user()->cannot($user_permissions['delete'])) {
            $actions->disableDelete();
        }
        if (Admin::user()->cannot($user_permissions['edit'])) {
            $actions->disableEdit();
        }
        if (Admin::user()->cannot($user_permissions['view'])) {
            $actions->disableView();
        }
    });
});
```

[laravel-admin](https://learnku.com/blog/know-nothing/tags/laravel-admin_10462)

> 本作品采用[《CC 协议》](https://learnku.com/docs/guide/cc4.0/6589)，转载必须注明作者和本文链接
