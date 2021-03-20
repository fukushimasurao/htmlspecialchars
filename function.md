

基本的に、formから入力されたものを出力する場合は、
`htmlspecialchars`をくっつけて、出力してください。

例：
```php
<?php
$name = $_POST['name'];
$mail = $_POST['mail'];
$pw = $_POST['pw'];
?>
<html>

<head>
    <meta charset="utf-8">
    <title>POST（受信）</title>
</head>

<body>
    お名前：<?= htmlspecialchars($name, ENT_QUOTES); ?>
    EMAIL：<?= htmlspecialchars($mail, ENT_QUOTES); ?>
    パスワード：<?= htmlspecialchars($pw, ENT_QUOTES); ?>
    <ul>
        <li><a href="index.php">index.php</a></li>
    </ul>
</body>

</html>
```

けど毎回毎回`htmlspecialchars`を書くのが面倒なので、関数化することも可能です。

1. `funcs.php`を作成する。
2. `funcs.php`の中に以下を記載

```php
<?php
//funcs.php

function h($str){
    return htmlspecialchars($str, ENT_QUOTES);
}
?>
```

3. `htmlspecialchars`を利用したいファイルの任意の場所(利用する箇所より上の行)に以下記載
```php
require_once('funcs.php');
```
※funcs.phpを設置する場所により`保存場所/funcs.php`みたいに書き換えてください。
これで、`funcs.php`に記載した内容を利用することができます。

4. htmlspecialcharsで出力したい内容を以下のように `h()`で囲ってあげる。
```php
<?php

// ↓追加
require_once('funcs.php')

$name = $_POST['name'];
$mail = $_POST['mail'];
$pw = $_POST['pw'];
?>
<html>

<head>
    <meta charset="utf-8">
    <title>POST（受信）</title>
</head>

<body>
    お名前：<?= h($name); ?>
    EMAIL：<?= h($mail); ?>
    パスワード：<?= h($pw); ?>
    <ul>
        <li><a href="index.php">index.php</a></li>
    </ul>
</body>

</html>
```
