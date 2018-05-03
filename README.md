# Hello Clojure

```
(println "hello world!")
```

## Syntax Exercises

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