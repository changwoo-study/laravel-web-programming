# Chapter 04: 뷰와 데이터 바인딩

`routes/web.php` 파일에 `Route::get()` 메소드로 뷰를 반한하는 코드를 작성해 봤다.
뷰 파일은 *리소스*로서 `resources/views` 디렉토리에 위치한다.

이 장에서는 뷰와 데이터를 넣는 방법에 대해 간략히 소개한다.

## 뷰 반환하기

```php
<?php
Route::get('/', function () {
   return view('errors.503'); 
});
```

* 하위 디렉토리는 '/'를 이용하거나 '.' 으로 참조 가능하다. 
* 템플릿 에서 `.blade.php` 부분은 생략한다. 그러나 만약 블레이드를 사용하지 않는다면 .php 확장자를 붙인 전체
  이름으로 줄 수도 있다.
  

## 데이터 바인딩
with() 메소드나 view() 메소드에서 설정 가능하다. 아래의 예를 참고한다.

```php
<?php
# case 1: with()
Route::get('/', function () {
    return view('welcome')->with('name', 'Foo');
});

# case 2: with()
Route::get('/', function () {
    return view('welcome')->with([
        'name'     => 'Foo',
        'greeting' => '안녕하세요',
    ]);
});

# case 3: view()
Route::get('/', function () {
    return view('welcome', [
        'name'     => 'Foo',
        'greeting' => '안녕하세요',
    ]);
});
```
