# Effective Modern C++勉強会


## 資料置き場

### [第1回 2015/1/28](https://atnd.org/events/60511)

* Item 1, 2 : [@herumi](https://twitter.com/herumi), [templateとautoの型推論](http://www.slideshare.net/herumi/template-44013078)
* Item 3, 4 : [@starpoz](https://twitter.com/starpoz)
* Item 5, 6 : [@redboltz](https://twitter.com/redboltz)

### [第2回 2015/2/25](https://atnd.org/events/62014)

* Item 7, 8 : [@Talos208](https://twitter.com/Talos208)
* Item 9, 10 : [@uchan_nos](https://twitter.com/uchan_nos)
* Item 11, 12 : 募集中

### コメント(随時思い出したら書く)

## Item 6のvector<bool>のoperatorをautoで受けると駄目な話。

[item6-1.cpp](https://github.com/herumi/emcjp/blob/master/src/item6-1.cpp)
VecがintではなくRefを返す。
intで受けるとRef()からintに変換されてから一時オブジェクトのVecとRefが消滅する。

autoで受けるとRef()のままになり、Refの寿命はあるけどそれが参照しているVecは先に消滅するのでそのあとintに変換するとアウト。
```
use int
Vec cstr
Ref cstr
read x
Ref dstr
Vec dstr
type=int a=5
use auto
Vec cstr
Ref cstr
Vec dstr
read x
type=struct Ref a=5
Ref dstr
```
