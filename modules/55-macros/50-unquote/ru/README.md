Попробуем решить еще одну задачку, создадим макрос, который принимает вектор чисел, суммирует их, а потом вычитает из суммы этот же вектор. Если бы мы писали функцию, то она выглядела бы так:

```clojure
(defn strange-fn [coll]
  (apply - (apply + coll) coll))

(strange-fn [1 2 3 4])
0
```

Раз мы хотим решить задачу через макрос, то последней формой, которую он будет возвращать, будет символы `apply`, `+` и `-`, поэтому применим оператор цитирования к последней форме, которую возвращаем:

```clojure
(defmacro strange-macro [coll]
  `(apply - (apply + coll) coll))

(strange-macro [1 2 3 4])
Could not resolve symbol: coll
```

Ох, нам нужно значение, которое хранится в `coll`, но как же получить это значение?

Для того чтобы подсказать Clojure, что внутри макроса при цитировании нужно вычислить, используется оператор `~` (unquote). Этот оператор используется вместе с оператором цитирования `'`, можно сказать, что он отменяет цитату в процитированном макросе (сложности перевода со словом unquote).

Теперь попробуем на другом примере новый оператор:

```clojure
; получим сумму двух сумм элементов вектора
(defmacro twice-sum-macro [coll]
  `(+ (apply + ~coll) (apply + ~coll)))

(twice-sum-macro [1 2 3 4])
20
```

Как видно из примера, мы воспользовались оператором `~`, для вычисления значения, которое хранилось в `coll`. Однако из-за того, что мы теперь производим зависимые вычисления внутри формы (зависимость от переданных аргументов), которую возвращаем, не получится воспользоваться формами `macroexpand` и `macroexpand-1`.

```clojure
(macroexpand twice-sum-macro)
Syntax error compiling at (REPL:1:1).
Can't take value of a macro: #'user/twice-sum-macro

(macroexpand-1 twice-sum-macro)
Syntax error compiling at (REPL:1:1).
Can't take value of a macro: #'user/twice-sum-macro
```