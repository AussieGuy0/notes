# Clojure

## Syntax
A note on terminology: Often valid clojure code is called a *form*, the term
*expression* may also be used.

There are two types of structures:

1. Literal representations of data structures 
(e.g 1, "string", ["vector", "of", "strings"]

2. Operations

Operations looks like: 

```
(operator operand1 operand2 ... operandn)
```

A basic operation:
```clojure
(+ 1 2)
```
Will add the operand 1 and 2 and return the result.


### if
```
(if boolean-form
  then-form
  else-form)
```
'boolean-form' is a form that evaluates to truthy or falsey.

'else-form' may be omitted, in that case, `nil` will be returned if the
boolean-form is false.


### do
```
(do operand1 operand2...)
```
`do` allows us to wrap multiple forms and run each of them.

Example:
```clojure
(if true
  (do (println "Was True!")
    "All good")
  (do (println "Was False!")
    "All bad"))
```

### when
```
(when boolean-form
  then-form1
  then-form2...
)
```
A combination of `if` and `do`, but with no 'else' branch.

### nil
`nil` is like `null` in Java.

We can check if something is `nil` via `nil?`

```clojure
(nil? 1)
```

### truthy/falesy
- falsey: `false`, `nil`
- truthy: eveything else

### boolean operators
- `=`: `(= 1 1)`
- `or`: returns either first truthy value (if exists), else last value

example:
```clojure
(or false nil :something :something_else)
```
Returns: `:something`

```clojure
(or false nil)
```
returns `nil`, as there are no truthy falues and the last value is `nil`


- `and`: returns either first falsey value (if exists), else the last truthy value
```clojure
(and :a :b)
```
returns `:b`

```clojure
(and :a nil :b false)
```
returns `nil`

### def
```
(def names ["adam", "brad", "charlie"])
```
Binds a name to a value.

Similar to assigining a variable in other languages. The terminology is avoided
though as reassigning names is frowned upon.

## Data structures

### Keywords
```clojure
:a_keyword
```
Often used as keys to maps. They are interned, so all instances of a keyword is
identically the same object.

### Maps
Empty: `{}`


Associating `:first_name` with `"Charlie"` and `last_name` with `"Smith"`
```clojure
{:first_name "Charlie", :last_name "Smith"}
```

Associating `"string-key"` with `+` function
```clojure
{"string-key" + }
```

Getting value from map:
```clojure
(get {:key "value"} :key "default-value")
```
or
```clojure
({:key "value"} :key)
```


### Vectors
Similar to an array. 
```clojure
[3 2 1]

(vector 3 2 1) ; => [3, 2, 1]

["a" :c 3] ; Vectors can contain different types

(get [3 2 1] 0)  ; => 3

(conj [3 2 1] 0) ; => [3 2 1 0]
```

### Lists
Similar to Vectors. Can be thought of as a linked list.

Choose lists when you want to efficently add items to the begnning. Also
a list should be used when writing a macro

```clojure
'(1 2 3 4)

(list :a 1) ; => (:a 1)

(nth (:a :b) 1) ; => :b

; Elements are added at beginning of a list
(conj `(1 2 3) 4) ; => (4 1 2 3)
```

### Sets
As with other languages, Sets are a collection of unique values.

Clojure has 2 kinds of sets: hash sets and sorted sets.

```clojure
#{:a :b}  ; hash set

(hash-set 1 1 2 2) ; => #{1 2}

(set [1 1 2 2]) ; => #{1 2}

(contains? #{:a :b} :a) ; => true

(:a #{:a :b}) ; => :a

(get #{:a :b} :a) ; => :a

```

### Functions

```clojure
; Defining a function
(defn do-something
  "A docstring that describes the function"
  [parameter]
  (str "do" "something"))
  
; Anonymous function
(fn [param-list] function-body)

(map (fn [num] (inc num)) [1,2,3]) ; # => (2 3 4)
(map #(inc %) [1,2,3]) ; # => (2 3 4)
```

## Core Functions
### filter vs take-while
```clojure
(filter #(< % 3) [1, 2, 4, 2]) ; # => (1 2 2)
(take-while #(< % 3) [1, 2, 4, 2]) ; # => (1 2)
```

## Leiningen
Used to create/run/build the project. A bit like Maven!

### Commands
**Create New Project**
```
lein new app project-name
```

**Run Project***
```
lein run
```

**Build Project**
```
lein uberjar
```

**REPL**
```
lein repl
```
