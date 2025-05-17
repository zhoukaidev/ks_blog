## 类型转换简介

类型转换这里主要包含两个概念:

* 某个实例是否是某种类型
* 根据继承关系，将某个对象转换成它的父类或其他子类

类型转换使用了两个操作符:

* `is`操作符(类型检查)
* `as`操作符(类型转换)

## 定义父类与子类用于类型转换

> 以下示例代码来自: [swift.type_casting](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html)

* 定义基类`MediaItem`

```swift
class MediaItem {
    var name: String  // 包含name属性
    init(name: String) { // init函数
        self.name = name
    }
}
```

* 定义子类`Movie`和`Song`

```swift
class Movie: MediaItem {
    var director: String
    init(name: String, director: String) {
        self.director = director
        super.init(name: name)
    }
}

class Song: MediaItem {
    var artist: String
    init(name: String, artist: String) {
        self.artist = artist
        super.init(name: name)
    }
}
```

* 创建数组存储相关实例

以下创建了`library`数组,并存储了两个`Movie`实例及一个`Song`实例。根据类型推断规则，这两个实例用于共同的父类`MediaItem`，所以
这里数组会被推断为[MediaItem]类型,相当于`let library:[MediaItem] = [xxx]`

```swift
let library = [
    Movie(name:"Casablanca", director: "Michael Curtiz"),
    Song(name: "Blue Suede Shoes", artist: "Elvis Presley"),
    Movie(name: "Citizen Kane", director: "Orson Welles")
]
```

## 类型检查

使用`is`操作符来检查一个实例能否转换成相应的子类类型。

```swift
var movieCount = 0
var songCount = 0
for item in library {
    // 执行向下类型转换，判断是否是Movie类型
    // 对于熟悉C++的人而言，是动态类型转换
    if item is Movie { 
        movieCount += 1
    } else if item is Song { // 判断是否是Song类型
        songCount += 1
    }
}

print("Media library contains: \(movieCount) movies and \(songCount) songs")
```

## 向下类型转换

在类的继承关系图中，通常将子类放在父类下面，所以通过将父类向子类的转换称为
向下类型转换。

```
      +------------+
      | base class |
      +------------+
            |
            |
            |
           \|/
      +------------+
      | subclass   |
      +------------+ 
```

通过使用(`as?`)或(`as!`)来实现向下类型转换。

使用`as?`执行向下类型转换时，会返回`Optional`类型，当向下类型转换失败的时候,
会返回`nil`值。

使用`as!`来执行向下类型转换时，如果类型转化失败，会触发`runtime error`.

```swift
for item in library {
    if let movie = item as? Movie {
        print("Movie: \(movie.name), dir: \(movie.director)")
    } else if let song = item as? Song {
        print("Song: \(song.name), by \(song.artist)")
    }
}
```
