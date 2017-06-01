# htmlMarkup
A HTML DOM parser written in PHP7+ let you manipulate HTML-Node-Objects.

## API Documentation

http://doc.alvine.io/de/alvine.markup.html/component/snapshot/

## Install and running htmlMarkup

Download Library from http://download.alvine.io

```bash
wget http://download.alvine.io/alvine.markup.html-<version>.phar
wget http://download.alvine.io/alvine.markup.html-<version>.phar.pubkey
````

## Usage

### simple output

 ```php

$html = \Alvine\Markup\Html\Fragment::getInstanceFromString('<b><i>Auto</i></b>');
echo (string) $html;
    
```

```html
<b><i>Auto</i></b>
```

### dom-manipulation

 ```php
$html = \Alvine\Markup\Html\Fragment::getInstanceFromString('<b><i>Auto</i></b>');
 
/** div und Text einhängen */
$html->current()
    ->appendChild((new \Alvine\Markup\Html\Element\Html\Div())
    ->appendChild(new \Alvine\Markup\Html\Node\Text('Hallo World!')));
 
echo (string) $html;
```

```html
<b><i>Auto</i><div>Hallo World!</div></b>
```

### HTML-Operations

```html
<div>
  <p data-replace="dataset:text | strtolower | trim">My World</p>
</div>
```

```html
<div>
  <a data-attributes="href dataset:url | index:2 | strtolower, title string:Mein Titel | trim">My World</a>
</div>
```

### Simple HTML-Operations

```php
$html = <<<EOF
<div>
  <p data-replace="dataset:url">url</p>
</div>
EOF;
 
echo (new \Alvine\Markup\Html\Engine())
    ->setDataset((new \Alvine\Markup\Html\Dataset)
        ->setValue('url', new \Alvine\Net\Resource\URI('http://www.example.com')))
    ->getHTML($html);
```

```html
<div>
  <p>http://www.example.com</p>
</div>
```

### Querys aka jquery

```php
echo (string) $fragment->find(new Selector('#opt2[class]'));
echo (string) $fragment->find(new Selector('li[class!="selected"]'));
```

## Documentation

https://wiki.schukai.com/display/alvine2/HTML+-+Programmierung
