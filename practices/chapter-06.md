# Chapter 06: 데이터베이스와 모델

## 데이터베이스와 사용자 생성
* DB: myapp 
* USER: homestead
* PASSWD: <지정한 패스워드>

posts 테이블 생성
```mysql
CREATE TABLE posts (
  id    INT(11) UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255),
  body  TEXT
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
```

## tinker 콘솔 사용
드디어 라라벨의 REPL 사용이다.

`php artisan tinker`


## .env 설정
아래 DB 설정을 확인한다.
```
DB_DATABASE=myapp
DB_USERNAME=homestead
DB_PASSWORD=<secret>
```

## INSERT
```
>>> DB::insert('INSERT INTO posts (title, body) VALUES (?, ?)', ['Hello Database', 'Greetings from tinker']);
=> true
>>> DB::insert('INSERT INTO posts (title, body) VALUES (?, ?)', ['Ola Database', 'Saludos de tiner']);
=> true
``` 


## SELECT
```
>>> DB::select('SELECT * FROM posts');
=> []

# 인서트 후 
>>> $posts = DB::select('SELECT * FROM posts');
=> [
     {#2863
       +"id": 1,
       +"title": "Hello Database",
       +"body": "Greetings from tinker",
     },
     {#2860
       +"id": 2,
       +"title": "Ola Database",
       +"body": "Saludos de tiner",
     },
   ]
>>> $posts[0]->title
=> "Hello Database"
```


## 쿼리 빌더

### get()
```
>>> DB::table('posts')->get();
=> Illuminate\Support\Collection {#2863
     all: [
       {#2866
         +"id": 1,
         +"title": "Hello Database",
         +"body": "Greetings from tinker",
       },
       {#2865
         +"id": 2,
         +"title": "Ola Database",
         +"body": "Saludos de tiner",
       },
     ],
   }
```

### first()

```
>>> DB::table('posts')->first();
=> {#2870
     +"id": 1,
     +"title": "Hello Database",
     +"body": "Greetings from tinker",
   }
```


### find()
```
>>> DB::table('posts')->find(2);
=> {#2867
     +"id": 2,
     +"title": "Ola Database",
     +"body": "Saludos de tiner",
   }
```


### where()
아래는 모두 같은 결과를 낸다.
```
>>> DB::table('posts')->where('id', '=', 1)->get();
>>> DB::table('posts')->where('id', 1)->get();
>>> DB::table('posts')->whereId(1)->get();
>>> DB::table('posts')->where(function ($query) {$query->where('id', 1);})->get();
=> Illuminate\Support\Collection {#2881
     all: [
       {#2878
         +"id": 1,
         +"title": "Hello Database",
         +"body": "Greetings from tinker",
       },
     ],
   }

```

'whereId()'는 동적 메소드이다. 낙타표기법으로 필드를 사용가능하다.


## 그 외에 
* [쿼리 빌더 공식 문서](https://laravel.com/docs/queries)
* [라라벨 API (5.7)](https://laravel.com/api/5.7/)
