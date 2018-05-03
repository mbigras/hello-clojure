# Hello Clojure

* [Syntax](#syntax)
* [Functions](#functions)

```
(println "hello world!")
```

## Syntax

https://clojure.org/guides/learn/syntax#_test_your_knowledge

Using the REPL, compute the sum of 7654 and 1234.

```
(+ 7654 1234)
```

Rewrite the following algebraic expression as a Clojure expression: ( 7 + 3 * 4 + 5 ) / 10.

```
; ( 7 + 3 * 4 + 5 ) / 10 = 2.4
(float (/ (+ 7 (* 3 4) 5) 10))
```

Using REPL documentation functions, find the documentation for the rem and mod functions. Compare the results of the provided expressions based on the documentation.

```
(doc rem)
(doc mod)
```

What does "Truncates toward negative infinity" mean?

Using find-doc, find the function that prints the stack trace of the most recent REPL exception.

```
(find-doc "trace")
user=> ("foo" 2 3)
ClassCastException java.base/java.lang.String cannot be cast to clojure.lang.IFn  user/eval210 (NO_SOURCE_FILE:31)
user=> (pst)
ClassCastException java.base/java.lang.String cannot be cast to clojure.lang.IFn
	user/eval210 (NO_SOURCE_FILE:31)
	user/eval210 (NO_SOURCE_FILE:31)
	clojure.lang.Compiler.eval (Compiler.java:7062)
	clojure.lang.Compiler.eval (Compiler.java:7025)
	clojure.core/eval (core.clj:3206)
	clojure.core/eval (core.clj:3202)
	clojure.main/repl/read-eval-print--8572/fn--8575 (main.clj:243)
	clojure.main/repl/read-eval-print--8572 (main.clj:243)
	clojure.main/repl/fn--8581 (main.clj:261)
	clojure.main/repl (main.clj:261)
	clojure.main/repl-opt (main.clj:325)
	clojure.main/main (main.clj:424)
nil
```

## Functions

https://clojure.org/guides/learn/functions#_test_your_knowledge

1) Define a function greet that takes no arguments and prints "Hello".

```
(defn greet [] (println "Hello"))
(greet)
```

2) Redefine greet using def, first with the fn special form and then with the #() reader macro.

```
;; using fn
(def greet (fn [] (println "Hello")))

;; using #()
(def greet #(println "Hello"))
```

3) Define a function greeting which:

Given no arguments, returns "Hello, World!"

Given one argument x, returns "Hello, x!"

Given two arguments x and y, returns "x, y!"

```
;; Hint use the str function to concatenate strings
(doc str)

(defn greeting
  ([] "Hello, World!")
  ([x] (str "Hello, " x "!"))
  ([x y] (str x ", " y "!")))

;; For testing
(assert (= "Hello, World!" (greeting)))
(assert (= "Hello, Clojure!" (greeting "Clojure")))
(assert (= "Good morning, Clojure!" (greeting "Good morning" "Clojure")))
```

4) Define a function do-nothing which takes a single argument x and returns it, unchanged.

```
(defn do-nothing [x] x)
```

In Clojure, this is the identity function. By itself, identity is not very useful, but it is sometimes necessary when working with higher-order functions.

```
(source identity)
```

5) Define a function always-thing which takes any number of arguments, ignores all of them, and returns the keyword :thing.

```
(defn always-thing [& all] :thing)
```

6) Define a function make-thingy which takes a single argument x. It should return another function, which takes any number of arguments and always returns x.

```
(defn make-thingy [x]
  (fn [& all] x))
((make-thingy 'cats) "foo" "bar" "baz")
cats

;; Tests
(let [n (rand-int Integer/MAX_VALUE)
      f (make-thingy n)]
  (assert (= n (f)))
  (assert (= n (f :foo)))
  (assert (= n (apply f :foo (range)))))
```

In Clojure, this is the constantly function.

```
(source constantly)
```

7) Define a function triplicate which takes another function and calls it three times, without any arguments.

(defn triplicate [f] ((f) (f) (f)))
(defn triplicate [f] (dotimes [n 3] (f)))

how to call a clojure function 3 times?

8) Define a function opposite which takes a single argument f. It should return another function which takes any number of arguments, applies f on them, and then calls not on the result. The not function in Clojure does logical negation.

```
(defn opposite [f]
  (fn [& args] (not (apply f args))))
```

In Clojure, this is the complement function.

```
(defn complement
  "Takes a fn f and returns a fn that takes the same arguments as f,
  has the same effects, if any, and returns the opposite truth value."
  [f]
  (fn
    ([] (not (f)))
    ([x] (not (f x)))
    ([x y] (not (f x y)))
    ([x y & zs] (not (apply f x y zs)))))
```

9) Define a function triplicate2 which takes another function and any number of arguments, then calls that function three times on those arguments. Re-use the function you defined in the earlier triplicate exercise.

(defn triplicate2 [f & args]
  (triplicate ___))

10) Using the java.lang.Math class (Math/pow, Math/cos, Math/sin, Math/PI), demonstrate the following mathematical facts:

* The cosine of pi is -1
* For some x, sin(x)^2 + cos(x)^2 = 1

```
(Math/cos Math/PI)
(defn f [x]
  (+
    (Math/pow (Math/sin x) 2)
    (Math/pow (Math/cos x) 2)))
```

11) Define a function that takes an HTTP URL as a string, fetches that URL from the web, and returns the content as a string.

Hint: Using the java.net.URL class and its openStream method. Then use the Clojure slurp function to get the content as a string.

https://gist.github.com/yang-wei/f4b38bff97f9fcad659c3fa7491ad73f

```
(defn http-get [url]
  (slurp
    (.openStream
      (java.net.URL. url))))

(assert (.contains (http-get "http://www.w3.org") "html"))
```

In fact, the Clojure slurp function interprets its argument as a URL first before trying it as a file name. Write a simplified http-get:

```
(defn http-get [url]
  (slurp url))
```

12) Define a function one-less-arg that takes two arguments:

* f, a function
* x, a value

and returns another function which calls f on x plus any additional arguments.

```
(defn cats [x y] (list x y))

(defn one-less-arg [f x]
  (fn [& args] (apply f x args)))

((one-less-arg cats "foo") "bar")
("foo" "bar")
```

In Clojure, the partial function is a more general version of this.

```
(doc partial)
((partial cats "flap") "jacks")
("flap" "jacks")

13) Define a function two-fns which takes two functions as arguments, f and g. It returns another function which takes one argument, calls g on it, then calls f on the result, and returns that.

That is, your function returns the composition of f and g.

(defn two-fns [f g]
  (fn [x] (f (g x))))
user=> (defn cats [x] (str "cats" x))
#'user/cats
user=> (defn dogs [x] (str "dogs" x))
#'user/dogs
user=> (two-fns cats dogs)
#object[user$two_fns$fn__191 0x5c0f79f0 "user$two_fns$fn__191@5c0f79f0"]
user=> ((two-fns cats dogs) "ants")
"catsdogsants"
user=>
```