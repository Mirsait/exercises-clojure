Создайте функцию `freq`, которая принимает коллекцию элементов и создает хеш-мапу с частотой появления элементов в коллекции. Больше подробностей в примерах.

```clojure
(freq ["a" "b" "c" "a" "a" "c" "a" "d" "b"])
; => {"a" 4, "b" 2, "c" 2, "d" 1}

(freq [])
; => {}

(freq ["Clojure" "Ruby" "Clojure" "Elixir" "Ruby" "HTML" "JS"])
; => {"Clojure" 2, "Ruby" 2, "Elixir" 1, "HTML" 1, "JS" 1}

(freq [10 10 10 20 300 41 53])
; => {10 3, 20 1, 300 1, 41 1, 53 1}

(freq [:a :b :c :d :a :a])
; => {:a 3, :b 1, :c 1, :d 1}
```