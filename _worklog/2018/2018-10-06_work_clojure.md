# clojure

```
$ lein new wornderland
$ cd wonderland
$ lein repl
```

# clojure expression 클로저 식

simple value
literal

```clojure
42
12.34
1/3
4/2
4.0/2
(/ 1 3)
1/3.0
(/ 1 3.0)

simple value
"jam"
keyword
:jam

"j"
\j

true
false

nil

(+ 1 (+ 8 3))

list
vector
map
set

idiomatic.
(1 2 "jam" :normalade-jar)
unidiomatic
(1, 2, "jam" :bee)


(first '(1 2 "jam" :bee))
(last '(1 2 "jam" :bee))
(rest '(1 2 "jam" :bee))
(last (rest '(1 2 "jam" :bee)))
(cons 1 '(1 2 "jam" :bee))
(cons 1 nil)
(cons 1 (cons 2 nil))
[:jar1 1 2 3 :jar2]
(nth [:jar1 1 2 3 :jar2] 0)
(nth [:jar1 1 2 3 :jar2] 1)
(nth [:jar1 1 2 3 :jar2] 2)
(first [:jar1 1 2 3 :jar2])
(last [:jar1 1 2 3 :jar2])

불변immutable 종속적persistent
cons 사용시 새 컬렉션 반환


(count [1 2 3 4])
(conj [:toast :butter 1 2]  :jam)
(conj '(:toast :butter 1 2)  :jam)

{:jam1 "strawberry" :jam2 "blackberry"}
{:jam1 "strawberry" :jam2 :blackberry}
{:jam1 "strawberry", :jam2 :blackberry}
{"jam1" "strawberry", :jam2 :blackberry}
(get {:jam1 "strawberry" :jam2 "blackberry"} :jam1)
(get {"jam1" "strawberry", :jam2 :blackberry} :jam1)
(get {"jam1" "strawberry", :jam2 :blackberry} "jam1")

(keys {:jam1 "strawberry" :jam2 "blackberry"})
(vals {:jam1 "strawberry" :jam2 "blackberry"})

(assoc {:jam1 "strawberry" :jam2 "blackberry"} :jam2 "orange")
(dissoc {:jam1 "strawberry" :jam2 "blackberry"} :jam2)

(merge {:jam1 "strawberry" :jam2 "blackberry"}
  {:jam3 "strawberry" :jam4 "blackberry"}
)

#{:red :blue :white :pink}

(clojure.set/union #{:r :g :b} #{:w :p :y})
(clojure.set/difference #{:r :g :b :w} #{:w :p :y})
(clojure.set/intersection #{:r :g :b :w} #{:w :p :y})

(set [:r :g :b])
(set {:a 1 :b 2 :c 3})

(get #{:r :g :b} :r)
(get #{:r :g :b} :k)

키워드를 이용해서 가져오기
(:r #{:r :g :b})
집합을 함수로 사용
(#{:r :g :b} :r)

(contains? #{:rabbit :door :watch} :rabbit)
(conj #{:door :rabbit} :jam)
(disj #{:rabbit :door} :door)


계산
(+ 1 1)
리스트
'(+ 1 1)

전역var def
(def developer "Alice")
(def user/developer "Alice")
(let developer "Alice in Wonderland")
developer

지역 바인딩 let
(def developer "Alice")
(let [developer "Alice in Wonderland" rabbit "White Rabbit"]
 [developer rabbit])
developer

함수 만들기 defn
(defn follow-the-Rabbit
  []
  "Off we go!")

(defn shop-for-jams
  [jam1 jam2]
  {:name "jam-basket"
  :jam1 jam1
  :jam2 jam2})
(shop-for-jams :jam1 :jam2)
(shop-for-jams "" "")

익명함수 fn
(fn [] (str "Off we go" "!"))
((fn [] (str "Off we go" "!")))
(def follow-again (fn [] (str "Off we go" "!")))
(follow-again)
익명함수 단축 #
(#(str "Off we go" "!"))
(#(str "Off we go" "!" %) "again")
(#(str "Off we go" "!" %1%2) "again" "!")

네임스페이스
(ns alice.favfoods)
(def fav-food "strawberry jam")
*ns*
fav-food
alice.favfoods/fav-food

(ns rabbit.favfoods)
(def fav-food "lettuce soup")
*ns*
fav-food
rabbit.favfoods/fav-food
alice.favfoods/fav-food

(clojure.set/union #{:r :b :w} #{:w :p :y})
(require 'clojure.set)
(ns wonderland)
(require 'alice.favfoods :as af)
af/fav-food


```
