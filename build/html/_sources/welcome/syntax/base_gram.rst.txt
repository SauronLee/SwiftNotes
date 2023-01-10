語法
=====

``If-slse``
----------------

* Ifの後にbool型しかつけられない。（括弧 ``()`` は省略可能）
  
.. code-block:: swift
    :linenos:

    let age = 4
    if age >= 22{
        print("Get married")
    } else if age >= 18 {
        print("Go to school")
    } else {
        print("Just a child")
    }

``While``
------------

.. code-block:: swift
    :linenos:

    var num = 5
    while num > 0 {
        print("num is \(num)")
        num -= 1
    } // for five times

.. code-block:: swift
    :linenos:

    var num = -1
    repeat {
        print("num id \(num)")
    } while num > 0 // for once



``For``
----------------

閉区間演算子 `a...b means a <= range <= b`

.. code-block:: swift
    :linenos:

    let names = ["A","B","C","D"]
    for i in 0...3 {
        print(names[i])
    } // output: A,B,C,D

.. code-block:: swift
    :linenos:

    let range = 1...3
    for i in range {
        print(names[i])
    } // output: B,C,D

.. code-block:: swift
    :linenos:

    for var i in range {
        i += 5
        print(i)
    } //output: 6,7,8


半開放区間演算子 ``a..<b means a <= range < b``

.. code-block:: swift
    :linenos:

    for i in 1..<5 {
        print(i)
    } // output: 1,2,3,4


.. code-block:: swift
    :linenos:

    var functions: [() -> Int] = []
    for i in 1...3 {
        functions.append {i}
    }
    for f in functions {
        print(f())
    }
    // 1 2 3


for on ``Array``
~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:

    let names = ["A","B","C","D"]
    for i in names[0...3] {
        print(names[i])
    } // output: A,B,C,D
    for i in names[2...] {
        print(names[i])
    } // output: B,C,D
    for i in names[...1] {
        print(names[i])
    } // output: A,B


The other ``range`` method
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:
    
    let range = ...5
    range.contains(7)   // false
    range.contains(4)   // true
    range.contains(-3)  // true


The ``range`` type on <generic>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:
    
    let range1: ClosedRange<Int> = 1...3
    let range2: Range<Int> = 1..<3
    let range3: PartialRangeThrough<Int> = 5


String can also be used in the range method, but cannot in ``for-in``

.. code-block:: swift
    :linenos:
    
    let stringRange = "a"..."f"
    stringRange.contains("d")   //true
    stringRange.contains("h")   //false

Check if the character is in ASCII.

.. code-block:: swift
    :linenos:
    
    let characterRange: ClosedRange<Character> = "\0"..."~"
    characterRange.containes("G")   //true


Range method with interval

.. code-block:: swift
    :linenos:
    
    let hours = 11
    let hourInterval = 2
    for trickMark in stride(form: 4, though: hours, by: hourInterval){
        print(trickMark)
    }   // output: 4,6,8,10


``Switch``
----------

.. code-block:: swift
    :linenos:
    
    var number = 1
    switch number {
        case 1:
            print("number is 1")
        case 2:
            print("number is 2")
        default:
            print("number is other")
    }   // output: number is 1


``Switch`` with fallthrough
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:
    
    var number = 1
    switch number {
        case 1:
            print("number is 1")
            fallthrough
        case 2:
            print("number is 2")
        default:
            print("number is other")
    }
    // output: number is 1
    //         number is 2

.. Note::

.. code-block:: swift
    :linenos:
    var number = 1
    switch number { // Switch must be exhaustive
        case 1:
            print("number is 1")
        case 2:
            print("number is 2")
    }


Switch with enumerate
~~~~~~~~~~~~~~~~~~~~~~


.. code-block:: swift
    :linenos:

    enum Answer {case right, wrong}
    let answer = Answer.right
    switch answer {
        case Answer.right:
            print("right")
        case Answer.wrong:
            print("wrong")
    }
    // or （Since `answer` is already identified as type `Answer`）
    switch answer {
        case .right:
            print("right")
        case .wrong:
            print("wrong")
    }


``Switch`` with ``range``
~~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:
    
    let count = 62
    switch count {
        case 0:
            print("none")
        case 1..<5:
            print("a few")
        case 5..<12:
        print("several")
        case 12..<100:
            print("hundreds of ")
        case 100..<1000:
            print("many")
    }   // dozens of 


``Switch`` with ``tuple``
~~~~~~~~~~~~~~~~~~~


.. code-block:: swift
    :linenos:
    
    let point = (1, 1)
    switch point {
        case (0, 0):
            print("the origin")
        case (_, 0):
            print("on the x-axis")
        case (0, _):
            print("on the y-axis")
        case (-2...2, -2...2):
            print("inside the box")
        default:
            print("outside of the box")
    }   // inside the box

.. code-block:: swift
    :linenos:
    
    let point = (2, 0)
    switch point {
        case (let x, 0):
            print("on the x-axis with an x value of \(x)")
        case (0, let y):
            print("on the y-axis with an y value of \(y)")
        case let (x, y):
            print("somewhere else at (\(x), \(y))")
    }   // output: on the x-axis with an x value of 2


``Where``
----------

.. code-block:: swift
    :linenos:
    
    let point = (1, -1)
    switch point {
        case let (x, y) where x == y:
            print("on the line x == y")
        case let (x, y) where x == -y:
            print("on the line x == -y")
        case let (x, y):
            print("(\(x), \(y)) is just some arbitrary point")
    }   // output: one the line x == -y

.. code-block:: swift
    :linenos:
    
    var numbers = [10, -20, 30, -10]
    var sum = 0
    for num in numbers where num > 0 {
        sum += num
    }
    print(sum)  // output: 40


Defination of Function
------------------------

.. code-block:: swift
    :linenos:
    
    func pi() -> Double {
        return 3.14
    }
    // Parameters can only be constants`let`
    func sum(v1: Int, v2: Int) -> Int {
        return v1 + v2
    }
    sum(v1: 10, v2: 20)
    ```
    No return value
    ```swift
    func sayHello() -> Void {
        print("Hello")
    }
    // or
    func sayHello() -> () {
        print("Hello")
    }
    // or
    func sayHello() {
        print("Hello")
    }


Argument Label
----------------

.. code-block:: swift
    :linenos:
    
    func goToWork(at time: String) {
        print("this time is \(time)")
    }
    goToWork(at: "08:00")
    // output: this time is 8:00


Default Parameter Value
--------------------------------


.. code-block:: swift
    :linenos:
    
    func check(name: String = "nobody", age: Int, job: String = "none") {
        print("name=\(name), age=\(age), job=\(job)")
    }
    check(name: "Jack", age: 20, job: "Doctor")
    check(name: "Rose", age: 20, job: "Doctor")
    check(age: 20, job: "Batman")
    check(age: 20)


Variadic Parameter
--------------------------------

.. code-block:: swift
    :linenos:
    
    func sum(_ numbers: Int...) -> Int {
        var total = 0
        for number in numbers {
            total += number
        }
        return total
    }
    sum(10, 20, 30, 40) // output: 100



Function Overload
--------------------------------


.. code-block:: swift
    :linenos:
    
    func sum(v1: Int, v2: Int) -> Int {
        v1 + v2
    }
    func sum(v1: Int, v2: Int, v3: Int) -> Int {
        v1 + v2 + v3
    }
    func sum(v1: Int, v2: Double) -> Double {
        Double(v1) + v2
    }
    func sum(v1: Double, v2: Int) -> Double {
        v1 + Double(v2)
    }
    func sum(_ v1: Int, _ v2: Int) -> Int {
        v1 + v2
    }
    func sum(a: Int, b: Int) -> Int {
        a + b
    }
    sum(v1: 10, v2: 20) // 30
    sum(v1: 10, v2: 20, v3: 30) // 60
    sum(v1: 10, v2: 20.0) // 30.0
    sum(v1: 10.0, v2: 20) // 30.0
    sum(10, 20) // 30
    sum(a: 10, b: 20) // 30


Function Type As Parameter
--------------------------------

.. code-block:: swift
    :linenos:
    
    func sum(v1: Int, v2: Int) -> Int{
        v1 + v2
    }
    func difference(v1: Int, v2: Int) -> Int{
        v1 - v2
    }
    func printResult(_ mathFn: (Int, Int) -> Int, _ a: Int, _ b: Int) {
        print("Result: \(mathFn(a, b))")
    }
    printResult(sum, 5, 2)  // Result: 7
    printResult(difference, 5, 2)   // Result: 3


Higher-order function
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:
    
    func next(_ input: Int) -> Int {
        input + 1
    }
    func previous(_ input: Int) -> Int {
        input - 1
    }
    func forward(_ forward: Bool) -> (Int) -> Int {
        forward ? next : previous
    }
    forward(true)(3)    // 4
    forward(false)(3)   // 2


Typealias
----------------

.. code-block:: swift
    :linenos:
    
    typealias Byte = Int8
    typealias Short = Int16
    typealias Long = Int64

.. code-block:: swift
    :linenos:
    
    typealias Date = (year: Int, month: int, day: Int)
    func test(_ date: Date) {
        print(date.0)
        print(date.year)
    }
    test((2023, 1, 2))

.. code-block:: swift
    :linenos:
    
    typealias IntFn = (Int, Int) -> Int
    func difference(v1: Int, v2: Int) -> Int {
        v1 - v2
    }
    let fn: IntFn = difference
    fn(20,10) //10

    func setFn(_ fn: Int Fn) {}
    setFn(difference)

    func getFn() -> IntFn {difference}


Nested Function
----------------

.. code-block:: swift
    :linenos:
    
    func forward(_ forward: Bool) -> (Int) -> Int {
        func next(_ input: Int) -> Int {
            input + 1
        }
        func previous(_ input: Int) -> Int {
            input - 1
        }
        return forward ? next : previous
    }
    forward(true)(3)    // 4
    forward(false)(3)   // 2

``Guard``
-----------

.. code-block:: swift
    :linenos:
    
    func login(_ info: [String : String]) {
        guard let username = info["username"] else {
            print("enter your name")
        }
        guard let username = info["password"] else {
            print("enter your password")
        }
        // if username 
        // if password
        print("username: \(username)", "password: \(password)")
    }
    login(["username": "jack", "password": "123456"]) // username: jack password: 123456
    login(["password": "123456"]) // enter your name
    login(["username": "jack"]) // enter your password


Initializer
----------------

.. code-block:: swift
    :linenos:
        
    struct Point {
        var x: Int = 0
        var y: Int = 0
    }
    // ==
    struct Point {
        var x: Int
        var y: Int
        init() {
            self.x = 0
            self.y = 0
        }
    }


``Struct`` ==? ``Class``
--------------------------------

* ``Struct``: value type (as ``enumerate``)
  
  * pass parameters == deep copy
  
* ``Class```: pointer type (reference type)

Stack space

+-----------------------+--------------------+---------------+------------------------------------+
| Memory Address        | Memory Data        | Object        | Description                        |
+=======================+====================+===============+====================================+
| 0x10000               | 3                  | point         | point.x                            |
+-----------------------+--------------------+---------------+------------------------------------+
| 0x10008               | 4                  | point         | point.y                            |
+-----------------------+--------------------+---------------+------------------------------------+
| 0x10010               | 0x90000            | size          | address of Size object             |
+-----------------------+--------------------+---------------+------------------------------------+

Heap space

+-----------------------+--------------------+---------------+------------------------------------+
| Memory Address        | Memory Data        | Object        | Description                        |
+=======================+====================+===============+====================================+
| 0x90000               | 0x41a8             | size          | pointer type infomation            |
+-----------------------+--------------------+---------------+------------------------------------+
| 0x90008               | 0x20002            | size          | reference count                    |
+-----------------------+--------------------+---------------+------------------------------------+
| 0x90010               | 1                  | size          | size.weight                        |
+-----------------------+--------------------+---------------+------------------------------------+
| 0x90018               | 2                  | size          | size.height                        |
+-----------------------+--------------------+---------------+------------------------------------+
