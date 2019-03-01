# laravel-admin configx

## Installation

need to install laravel-admin-ext/config first, see https://github.com/laravel-admin-extensions/config

Then run :

```
$ composer require ichynul/configx
```

Then run:

```
$ php artisan admin:import configx
```

Add a tabs config in `config/admin.php`:

```php
    'extensions' => [
        'configx' => [
            // Set to `false` if you want to disable this extension
            'enable' => true,
            //
            'tabs' => [
                'base' => '基本设置',
                'shop' => '店铺设置',
                'uplaod' => '上传设置'
            ],
            // Whether check group permissions. if (!Admin::user()->can('confix.tab.base')) {/*hide base tab*/ } .
            'check_permission' => false
        ],
    ],

```

## Usage

Open `http://your-host/admin/configx`

## Demo

You can click "+" to add an new config key :

step 1 Select config type from `['base' , 'shop' , 'uplaod']`

step 2 Select form-element type from `['normal', 'date', 'time', 'datetime', 'image', 'yes_or_no', 'number', 'rate', 'editor', 'radio_group' ,'checkbox_group', 'select']`... and so on

step 3 If you selected form-element type is `['radio_group' ,'checkbox_group', 'select']` ,you need inupt `[options]` :

just text:

`text1`
`text2`
...

and key-text:

`key1 : text1`
`key2 : text2`

or load from ulr:

`options_url:/api/mydata`

If you selected form-element type is `textarea` , you can config it `rows:3` , default is 5.

If you selected form-element type is `table`, `rows / cols` is needed :

`base.some_key`

`rows : 4`
`cols : 4`

This wiil build a table like below :

```php
/*
|-------------------------------------------------------------------------------------
|  r_label\ c_labe |       c_label1      |        c_label2     |      c_label3       |  ⬅Col labels
|-------------------------------------------------------------------------------------
|     r_label1     |  base.some_key_1_1  |  base.some_key_1_2  |  base.some_key_1_3  |
|-------------------------------------------------------------------------------------
|     r_label2     |  base.some_key_2_1  |  base.some_key_2_2  |  base.some_key_2_3  |
|-------------------------------------------------------------------------------------
|     r_label3     |  base.some_key_3_1  |  base.some_key_3_2  |  base.some_key_3_3  |
|-------------------------------------------------------------------------------------
        ↑
    Ros labels

You can edit labels as you want.

Each <td> has a key , base.some_key_[0]_[0] to base.some_key_[rows-1]_[cols-1] . (from 0 to length -1 )

So, you can chang a label <td> to input :

|-------------------------------------------------------------------------------------
|  r_label\ c_labe |       c_label1      |        c_label2     |  base.some_key_0_3  |  ⬅ [c_label3 change] to [base.some_key_0_3] , we can input here .
|-------------------------------------------------------------------------------------     (可以把label 换成输入元素)
|     r_label1     |  base.some_key_1_1  |  base.some_key_1_2  |  base.some_key_1_3  |
|-------------------------------------------------------------------------------------
|     r_label2     |  base.some_key_2_1  |  base.some_key_2_2  |  base.some_key_2_3  |
|-------------------------------------------------------------------------------------
|     r_label3     |  base.some_key_3_1  |     hello world!    |  base.some_key_3_3  |
|-------------------------------------------------------------------------------------
                                                    ↑
                                    [base.some_key_3_2] change to [hello world!]
                                        , we can not input here any more ,
                                     it wiil just show label text 'hello world!' .
                                        (也可以把输入元素换成仅显示文字)

note : if text = key ,render as input form element , otherwise just show the text you leave.

总结 : 如果输入的字符串与td默认key一样，这个位置将是一个可输入的表单元素，否则就显示原样你输入的字符串 .

*/
```

Double click any area of form to sort the configs witch in the same group. (双击表单界面进入排序模式，可对同一分组下的配置排序)

The keys will start with tab-keys in config :

- base.site_name
- base.site_tel
- base.site_logo
- base.site_open
- ...
- shop.shipping_compnay
- shop.open_time
- shop.open_date
- ...
- uplaod.size_limit
- uplaod.allow_type
- ...

Add a lang config in `resources/lang/{zh-CN}/admin.php`

```php
'configx' => [
        'new_config_type' => '新配置类型',
        'new_config_key' => '新配置key',
        'new_config_element' => '新配置表单元素',
        'new_config_help' => '新配置help',
        'new_config_options' => '新配置扩展项',
        'header' => '网站设置',
        'desc' => '网站设置设置',
        'element' => [
           'normal' => '默认',
            'textarea' => '文本域',
            'date' => '日期',
            'time' => '时间',
            'datetime' => '日期时间',
            'image' => '图片',
            'multiple_image' => '多图',
            'file' => '文件',
            'multiple_file' => '多文件',
            'yes_or_no' => '是或否',
            'editor' => '编辑器',
            'radio_group' => '单选框组',
            'checkbox_group' => '多选框组',
            'number' => '数字',
            'rate' => '比例',
            'select' => '下拉框',
            'tags' => '标签',
            'icon' => '图标',
            'color' => '颜色',
            'table' =>'表格'
        ],
        'base' => [
            'site_name' => '网站名称',
            'site_tel' =>　'电话',
            'site_logo' => '网站logo',
            'site_open' => '网站开关'
        ],
        'shop' => [
            'shipping_compnay' => '公司名称',
            'open_time' =>　'开启时间',
            'open_date' => '开启日期'
        ],
        'uplaod' => [
            'size_limit' => '大小限制',
            'allow_type' =>　'允许类型'
        ],
    ],
'yes' => '是',
'no' => '否'
```

if you need add a new config tab, chang it in `config/admin.php`.

After add config in the panel, use `config($key)` to get value you configured.

License

---

Licensed under [The MIT License (MIT)](LICENSE).
