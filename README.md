# go-gimei

golang port of [gimei](https://github.com/willnet/gimei)

## Usage

```go
package main

import (
	"fmt"

	"github.com/mattn/go-gimei"
)

func main() {
	name := gimei.NewName()
	fmt.Println(name)                  // 斎藤 陽菜
	fmt.Println(name.Kanji())          // 斎藤 陽菜
	fmt.Println(name.Hiragana())       // さいとう はるな
	fmt.Println(name.Katakana())       // サイトウ ハルナ
	fmt.Println(name.Last.Kanji())     // 斎藤
	fmt.Println(name.Last.Hiragana())  // さいとう
	fmt.Println(name.Last.Katakana())  // サイトウ
	fmt.Println(name.First.Kanji())    // 陽菜
	fmt.Println(name.First.Hiragana()) // はるな
	fmt.Println(name.First.Katakana()) // ハルナ
	fmt.Println(name.IsMale())         // false

	male := gimei.NewMale()
	fmt.Println(male)            // 小林 顕士
	fmt.Println(male.IsMale())   // true
	fmt.Println(male.IsFemale()) // false

	address := gimei.NewAddress()
	fmt.Println(address)                       // 岡山県大島郡大和村稲木町
	fmt.Println(address.Kanji())               // 岡山県大島郡大和村稲木町
	fmt.Println(address.Hiragana())            // おかやまけんおおしまぐんやまとそんいなぎちょう
	fmt.Println(address.Katakana())            // オカヤマケンオオシマグンヤマトソンイナギチョウ
	fmt.Println(address.Prefecture)            // 岡山県
	fmt.Println(address.Prefecture.Kanji())    // 岡山県
	fmt.Println(address.Prefecture.Hiragana()) // おかやまけん
	fmt.Println(address.Prefecture.Katakana()) // オカヤマケン
	fmt.Println(address.Town)                  // 大島郡大和村
	fmt.Println(address.Town.Kanji())          // 大島郡大和村
	fmt.Println(address.Town.Hiragana())       // おおしまぐんやまとそん
	fmt.Println(address.Town.Katakana())       // オオシマグンヤマトソン
	fmt.Println(address.City)                  // 稲木町
	fmt.Println(address.City.Kanji())          // 稲木町
	fmt.Println(address.City.Hiragana())       // いなぎちょう
	fmt.Println(address.City.Katakana())       // イナギチョウ

	prefecture := gimei.NewPrefecture()
	fmt.Println(prefecture) // 青森県
}
```

### CLI

```bash
$ gimei [OPTIONS] [ARGS]
```

#### OPTIONS

```
-type string
    display instead of a mixed-gender personal name: 'male', 'female' or 'address'.
    if ARGS is omitted, display in kanji.
-sep separator
    field separator
```    

#### ARGS

````
Arguments for a personal name:

- 'kanji', 'hiragana', 'katakana'
    full name  
- 'last-kanji', 'last-hiragana', 'last-katakana'
    last name 
- 'first-kanji', 'first-hiragana', 'first-katakana'
    first name 
- 'is-male', 'is-female'
    'true' or 'false'

Arguments for an address:

- kanji / hiragana / katakana
    address
- 'prefecture-kanji', 'prefecture-hiragana', 'prefecture-katakana'
    prefecture
- 'town-kanji', 'town-hiragana', 'town-katakana'
    town
- 'city-kanji', 'city-hiragana', 'city-katakana'
    city
```

#### EXAMPLES

```bash
$ gimei
古賀 正浩
$ gimei name katakana
中村 紳一, ナカムラ シンイチ
$ gimei -type address -sep '/' prefecture-kanji town-kanji
滋賀県/田所町
```

### Deterministic Random

go-gimei supports seeding of its pseudo-random number generator to provide
deterministic output of repeated method calls.

```go
import "math/rand"

gimei.SetRandom(rand.New(rand.NewSource(42)))
fmt.Println(gimei.NewName())    // 前川 永麻
fmt.Println(gimei.NewAddress()) // 佐賀県斜里郡斜里町浄法寺町樋口

gimei.SetRandom(rand.New(rand.NewSource(42)))
fmt.Println(gimei.NewName())    // 前川 永麻
fmt.Println(gimei.NewAddress()) // 佐賀県斜里郡斜里町浄法寺町樋口

```

## Requirements

golang

## Installation

```
$ go get github.com/mattn/go-gimei
```

## Running Tests

To run all the tests, do:

```bash
$ go test
```

## License

MIT

Dictionary YAML file is generated from [naist-jdic](https://ja.osdn.net/projects/naist-jdic/).

## Author

Yasuhiro Matsumoto (a.k.a mattn)
