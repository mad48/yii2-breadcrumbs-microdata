Yii2 Breadcrumbs widget with Microdata from schema.org
=========================
Add Microdata markup to Yii2 breadcrumbs

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist mad48/yii2-breadcrumbs-microdata "*"
```

or add

```
"mad48/yii2-breadcrumbs-microdata": "*"
```

to the `require` section of your `composer.json` file.

Or just copy `BreadcrumbsMicrodata.php` into `common\widgets` folder.


Usage
-----

Find in you project (usually `frontend\views\layouts\main.php`):

```php
Breadcrumbs::widget([ ... ])
```

and change:

```php
BreadcrumbsMicrodata::widget([ ... ])
```

Add to top:
```php
use common\widgets\BreadcrumbsMicrodata;
```

Widget call:
-----
Fill breadcrumbs array in view:
```php
$this->params['breadcrumbs'][] = ['label' => 'Catalog', 'url' => ['catalog/']];
$this->params['breadcrumbs'][] = ['label' => 'Computers'];
```

or fill breadcrumbs array in controller:
```php
$this->view->params['breadcrumbs'][] = ['label' => 'Catalog', 'url' => ['catalog/']];
$this->view->params['breadcrumbs'][] = ['label' => 'Computers'];
```

An example of calling a widget:
```php
<?= BreadcrumbsWidget::widget([
    'options' => [
        'class' => 'breadcrumb',
    ],
    'homeLink' => [
        'label' => Yii::t('yii', 'Home'),
        'url' => ['/'],
        'class' => 'home',
        'template' => '<li>{link}</li>',
    ],
    'links' => isset($this->params['breadcrumbs']) ? $this->params['breadcrumbs'] : [],
    'itemTemplate' => '<li>{link}</li>',
    'activeItemTemplate' => '<li class="active">{link}</li>',
    'tag' => 'ul'
]);
?>
```
or simple
```php
<?= BreadcrumbsWidget::widget([
      'links' => isset($this->params['breadcrumbs']) ? $this->params['breadcrumbs'] : [],
 ]);
?>
```

Examples of output:
-----
Default widget (`yii\widgets\Breadcrumbs`) output:

```html
<ul class="breadcrumb">
    <li>
        <a class="home" href="/">Home</a>
    </li>
    <li>
        <a href="/catalog">Catalog</a>
    </li>
    <li class="active">
        Computers
    </li>
</ul>
```

Widget with Microdata (`common\widgets\BreadcrumbsMicrodata`) :

```html
<ul class="breadcrumb" itemscope="" itemtype="http://schema.org/BreadcrumbList">
    <li itemprop="itemListElement" itemscope="" itemtype="http://schema.org/ListItem">
        <a class="home" href="/" itemprop="item">
            <span itemprop="name">Home</span>
        </a>
        <meta itemprop="position" content="1">
    </li>
    <li itemprop="itemListElement" itemscope="" itemtype="http://schema.org/ListItem">
        <a href="/catalog" itemprop="item">
            <span itemprop="name">Catalog</span>
        </a>
        <meta itemprop="position" content="2">
    </li>
    <li class="active" itemprop="itemListElement" itemscope="" itemtype="http://schema.org/ListItem">
        <span itemprop="item">
            <span itemprop="name">Computers</span>
        </span>
        <meta itemprop="position" content="3">
    </li>
</ul>
```

License
----

[MIT](http://www.opensource.org/licenses/mit-license.php)