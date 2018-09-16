# Chapter 05: 블레이드

블레이드 템플릿 엔진에 대해 소개하는 장이다.
간단한 개념을 설명한다.

## 문법 개요

### 보간

`{{ $greetings or 'Hello' }}`

`{{ $greetings }}`

문자열 출력의 기본이다. 기본으로 이스케이프 된다.

이스케이프하지 않으려면,

`{!! $var !!}`

처럼 사용한다.

### 주석
`{{-- 주석 내용 --}}`

템플릿을 위한 주석이다.


### 제어: if

```
@if (condition)
    statement
@elseif (conditio)
    statement
@else
    statement
@endif
```


### 제어: looping

```
@foreach ($vars as $var)
    statement
@empty
    statement_when_vars_empty
@endforeach
```


### 상속
마스터 템플릿 (resources/views/layouts/master.blade.php)
```blade
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>라라벨 입문</title>
</head>
<body>
    @yield('content')
</body>
</html>
```
<br>
<br>

상속하는 템플릿 (resources/views/welcome.blade.php)
```blade
@extends('layouts.master')

@section('content')
    <p>저는 자식 뷰의 'content' 섹션입니다.</p>
@endsection
```


### 삽입

```blade
@extends('layouts.master')
@section('content')
    @include('partial.footer')
@endsection
```



### 섹션 상속
상속되는 곳에서 같은 섹션을 완전히 오버라이드 하거나 상속하는 섹션에 코드를 더할 수 있다.

```blade
@section('script')
    @parent
    <script>
        alert('조각 뷰의 alert section.');
    </script>
@endsection
```

## 더 알아보기 
* [라라벨 공식 문서 (5.7)](https://laravel.com/docs/5.7/blade)
* [라라벨 한국어 - 블레이드 탬플릿 (5.6)](https://laravel.kr/docs/5.6/blade)
