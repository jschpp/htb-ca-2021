# MiniSTRyplace

## Challenge

```plain
Let's read this website in the language of Alines. Or maybe not?
```

This challenge comes with a Dockerfile and the source for the site.

## Solution

The interesting part lies within the following lines:

```php
$lang = ['en.php', 'qw.php'];
        include('pages/' . (isset($_GET['lang']) ? str_replace('../', '', $_GET['lang']) : $lang[array_rand($lang)]));
    ?>
```

As you can see the above includes a file and the only input sanitation is
`str_replace`. A quick look inside the [documentation][strreplace] of that command reveals the
following warning:

```plain
Because str_replace() replaces left to right, it might replace a previously inserted value when doing multiple replacements.
```

Soo since `str_replace` only runs once and it replaces left to right it is quite
easy to construct an argument which will resolve into the path of the flag.

This class of bugs is called 'directory traversal bug'

Trying to open the following url will yield the flag:

```plain
?lang=.../...//.../...//flag
```

The reason that works, is that every `../` will be removed and leave the
following:

```plain
?lang=../../flag
```

Since the page trying to be loaded lies within `/www/pages` and the flag resides
here: `/flag` the above will nice return the flag.

[strreplace]: https://www.php.net/manual/en/function.str-replace.php
