# Chapter 03: 라우트 이름

웹 애플리케이션 분석 시 라우트는 매우 중요하다. 앱이 어떻게 동작하는지 분석하기 위한 이정표가 되기 때문이다.

이 장에서는 간단한 라우팅에 대한 설명을 한다.

## 라우팅 예제

`routes/web.php` 파일에는 이런 코드가 기본적으로 포함되어 있다.

```php
<?php
Route::get('/', function () {
    return view('welcome');
});
```

파라미터를 설정하기 위해서는 `{foo}`처럼 사용하는 것도 가능하다. 선택적인 인자임을 선언하기 위해서는 끝에 ?을 붙이고 핸들러
함수의 인자에 기본값을 부여할 수도 있다.
```php
<?php
Route::get('/{foo}', function ($foo) {
    return $foo; 
});
```


```php
<?php
Route::get('/{foo?}', function ($foo = 'bar') {
    return $foo; 
});
```


파라미터의 패턴을 지정하는 방법도 가능하다. 아래 두 가지 방법을 참고한다.
```php
<?php
Route::pattern('foo', '[0-9a-zA-Z\{3}');
Route::get('/{foo?}', function ($foo = 'bar') {
    return $foo;
});
```


```php
<?php
Route::get('/{foo?}', function ($foo = 'bar') {
    return $foo;
})->where('foo', '[0-9a-zA-Z\{3}');
```


이름을 지정하여 리버싱도 가능하게 할 수 있다.
```php
<?php
Route::get('/{foo}', [
    'as' => 'home',
    function () {
        return '제 이름은 "home"입니다.'; 
    }
]);

Route::get('/home', function () {
    return redirect(route('home'));
});
```