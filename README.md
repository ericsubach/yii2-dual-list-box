Dual list box Widget for Yii 2
==================================

`Dual list box Widget` is a wrapper for Dual List Box plugin for jQuery and Bootstrap,
Bootstrap Dual List Box is a dual list box implementation especially designed for Bootstrap and jQuery. This control is quite easy for users to understand and use. Also it is possible to work with very large multi-selects without confusing the user.

This version differes from the parent in that it works with json data pulls. Both the php/yii wrapper and the actual Javascript have been updated to get this working.

The MIT License (MIT)

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist esubach/yii2-dual-list-box "dev-master"
```

or (if you have composer in your path)

```
composer require --prefer-dist esubach/yii2-dual-list-box "dev-master"
```


or add

```
"esubach/yii2-dual-list-box": "dev-master"
```

to the require section of your `composer.json` file.


Usage
-----

Once the extension is installed, simply use it in your code:

## EXAMPLE ##

### View ###

```php

echo esubach\duallistbox\Widget::widget([
    'model' => $model,
    'attribute' => 'list_regions',
    'title' => 'Example Title',
    'data' => $region,
    'data_id'=> 'id',
    'data_value'=> 'name',
    'json_uri' => 'http://example.com/data',
    'lngOptions' => [
        'warning_info' => 'Are you sure you want to move this many items? Doing so can cause your browser to become unresponsive.',
        'search_placeholder' => 'Filter',
        'showing' => ' - showing',
        'available' => 'Available',
        'selected' => 'Selected'
    ]
  ]);
```

model - model for form
attribute - model attribute for form
title - view name for attribute

data - model (Region::find()->all()) OR array['id'=>1,'name'=>'']; **This is a change from the upstream project.** 
data_id - name attribute for id
data_value - name attribute for value

#### sample json data

```

[
    {
        "index": 0,
        "name": "Peters Sloan",
        "company": "Kongle",
        "email": "peterssloan@kongle.com",
        "selected": true
    },
    {
        "index": 1,
        "name": "Bailey Hoffman",
        "company": "Centrexin",
        "email": "baileyhoffman@centrexin.com",
        "visuals": "red"
    },
    {
        "index": 2,
        "name": "Christine Hahn",
        "company": "Geoform",
        "email": "christinehahn@geoform.com",
        "selected": false
    }
]
```

in this example, only Peters Sloan would be selected by default

#### To refresh the data or use a different data source

```
    $('#list_regions').update({
        uri: 'http://example.com/data2',
    });
```


### Controller VIEW ###

```php
        $model = new ModelForm;
        
        $region = Region::find()->all();
```

### Controller SAVE ###

```php
$model = new ModelForm;
$model->load(Yii::$app->request->post());
$region_model = Json::decode($model->list_regions);
```
