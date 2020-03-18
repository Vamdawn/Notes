# Clojure 数据结构与抽象

## list

Create

```clojure
; list字面值
()

; 构建由items构成的list
(list & items)

; 将前面的元素添加到list前构成新的list
(list* args)
(list* a args)
(list* a b c d & more)
```

Exmine

```clojure
; 返回集合中第一个元素，如果集合为空或nil则返回nil
(first coll)

; 返回给定下标位置的值
(nth coll index)            ; 下标越界 throw exception
(nth coll index not-found)  ; 下标越界 返回not found

; 对于list或queue，相当于first
; 对于空集合或者nil，返回nil
(peek coll)

; 可以使用java中list的操作函数
(.indexOf coll item)
(.lastIndexOf coll item)
```

Change

```clojure
; 返回一个新的sequence，x是第一个元素，seq是剩余部分
(cons x seq)

; 返回一个新的collection，xs被添加到coll中
; 对于list，conj将把xs添加到coll前面
(conj coll x)
(conj coll x & xs)

; 返回由coll除了第一个元素以外剩下元素构成的新sequence
; 返回的sequence可能为空
(rest coll)

; 对于list/queue，返回一个新的list/queue，由coll中除了第一个元素的剩下元素构成
; 当coll为空会throw exception
(pop coll)
```

## vector

Create

```clojure
; vector字面量
[]

; 构建由给定元素构成的vector
(vector)
(vector a)
(vector a b c d e f & args)

; 创建包含coll内容的vector
(vec coll)
; tips: 对java array使用(vec)将返回java array的别名，即后续改动会影响java array

; 创建一个由单一种基本类型元素构成的vector
; t取值下面其中之一:
; :int :long :float :double :byte :short :char :boolean
(vector-of t)
(vector-of t & elements)
; vector-of的使用目的是为了有效利用空间

; 对每一个coll的第一个/第二个/...依次应用函数f，直到colls中任意一个被执行完
; 返回由上述结果构成的vector
(mapv f coll)
(mapv f c1 c2 c3 & colls)
; 与高阶函数map相似，但是返回vector

; 返回经(pred item)检验结果为逻辑true的items构成的vector
(filterv pred coll)
```

Examine

```clojure
; 通过下标获取vector指定位置元素
(vec index)                 ; 下标越界 throw exception
(nth vec index)             ; 下标越界 throw exception
(nth vec index not-found)   ; 下标越界 返回not found
(get vec index)             ; 下标越界 返回nil
(get vec index not-found)   ; 下标越界 返回not found

; 对于vector，相当于last，但是效率更高
; 对于空集合或者nil，返回nil
(peek coll)

; 可以使用java中list的操作函数
(.indexOf coll item)
(.lastIndexOf coll item)
```

Change

```clojure
; 修改指定下标的值，返回修改后元素构成的新vector
; 对于vector，key相当于下标
; 使用该方法可以返回添加元素的vector，但是下标需要连续，否则会throw exception
(assoc map key val)
(assoc map key val & kvs)

; 修改嵌套关联结构下的值，并返回修改后的新vector
(assoc-in map [k & ks] v)

; 对于vector，返回一个新的vector，由coll中除了最后一个元素的剩下元素构成
; 当coll为空会throw exception
(pop coll)

; 返回一个新的vector，从v的[start, end)的元素构成
; 如果end不提供，默认为(count v)
; 越界/end<start时会throw exception: IndexOutOfBoundsException
(subvec v start)
(subvec v start end)
; tips: subvec的速度在O(1)级别
; tips: subvec会保留原vector的引用。所以当从一个大vector中获取得到子vector，原本的vector不会再使用，那么考虑使用(into [] x)将引用释放

; 给定一个由替换对构成的map，以及一个collection，返回一个vector/sequence，coll的元素=smap中一个key时，将其替换为smap对应的val。
; smap中不存在的key则不进行替换，保留原始状态
; 当coll未提供时，返回一个transducer
(replace smap)
(replace smap coll)

; 返回一个新的collection，xs被添加到coll中
; 对于vector，conj将把xs添加到coll后面
(conj coll x)
(conj coll x & xs)

; 返回一个sequence，由rev的元素顺序反向构成
; rev可以是vector或sorted-map
; rev为空则返回nil，rev为nil时会throw exception: NullPointerException
; 常数时间
(resq rev)

; 更新关系型结构中的一个值，k为key，f为函数，应用到旧的值上
; 传入key不存在时，nil将被传递作为f参数
; x y z & more作为f需要的剩余参数
(update m k f)
(update m k f x y z & more)

; 更新嵌套关系结构中的一个值
; 如果指定ks下的登记不存在，hash-maps将被创建
(update-in m ks f & args)
```

Oops

```clojure
; reduces一个关系型集合，f应该是有3个参数的函数
; 应用f到init，第1个key和coll中第1个值
; 应用f到前一次结果，第2个key和coll中第2个值
; ...
; 返回最后的结果
; reduce-kv支持vector，key为下标序数
(reduce-kv f init coll)
```

## set

## map
