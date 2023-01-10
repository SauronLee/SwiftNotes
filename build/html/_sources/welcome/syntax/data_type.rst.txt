データ・タイプ
============


定数と変数
---------

| ``let`` 定数はコンパイル時に決定する必要はありませんが、使用する前に一度だけ代入する必要があります。

.. code-block:: swift
    :linenos:

    var num = 10
    num += 20
    let age = num

.. code-block:: swift
    :linenos:

    func getAge() -> Int {
        return 10
    }
    let age = getAge()

定数や変数は、初期化されるまでは使用できません。

.. code-block:: swift
    :linenos:
    
    let age: Int
    var height: Int
    print(age) //error
    print(height) //error

データ型
---------

* value type
    - enum: Optional
    - struct: Bool, Int, Float, Double, Character, String, Array, Dictionary, Set
* reference type: class

| 整数型: Int8, Int16, Int32, Int64, UInt8, UInt16, UInt32, UInt64
| 最大値と最小値: Int.max, Int.min
| 小数型: Float 32桁, Double 64桁

.. code-block:: swift
    :linenos:

    let letFloat: Float = 30.0
    let letDouble = 30.0

Bool
~~~~~

.. code-block:: swift
    :linenos:

    let bool = true // or false

String
~~~~~~~

.. code-block:: swift
    :linenos:

    let string = "自然言語処理"

Character（ASCII, Unicode)
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:

    let character: Character = "😀" //emoji

Int
~~~~

.. code-block:: swift
    :linenos:

    let intDecimal = 17
    let intBinary = 0b10001
    let intOctal = 0o21
    let intHexadecimal = 0x11

Double
~~~~~~~

.. code-block:: swift
    :linenos:

    let doubleDecimal = 125.0 //or 1.25e2
    let doubleHexadecimal = 0xFp2 // means 15x2^2

Array
~~~~~~~

.. code-block:: swift
    :linenos:

    let array = [1,2,3,4]

* ``Array.sort()`` 

.. code-block:: swift
    :linenos:
    
    // `Array.sort()` defination
    func sort(by areInIncreasingOrder: (Element, Element) -> Bool)

e.g.

.. code-block:: swift
    :linenos:

    func cmp(i1: Int, i2: Int) -> Bool {
        return i1 > i2
    }
    var nums = [2,5,1,6,3,8,9]
    nums.sort(by: cmp)
    // [9,8,6,5,3,2,1]

.. code-block:: swift
    :linenos:

    nums.sort(by:{
        (i1: Int, i2: Int) -> Bool in return i1 < i2
    })
    nums.sort(by:{i1, i2 in return i1 < i2})
    nums.sort(by:{i1, i2 in i1 < i2})
    nums.sort(by:{$0 < $1})
    nums.sort(by: <)
    nums.sort() {$0 < $1}
    nums.sort {$0 < $1}
    //[1,2,3,5,6,8,9]

Dictionary
~~~~~~~~~~~

.. code-block:: swift
    :linenos:

    let dictionary = ["age" : 18, "height" : 168, "weight" : 120]

可読性
~~~~~~~~

.. code-block:: swift
    :linenos:

    100_000 == 100000 == 10_0000

タイプ変換
~~~~~~~~~

.. code-block:: swift
    :linenos:

    //整数
    let int1: Uint16 = 2_000
    let int2: UInt8 = 1
    let int3 = int1 + UInt16(int2)
    //小数
    let int = 3
    let double = 0.14
    let pi = Double(int) + double
    let intPi = Int(pi)
    //other
    let result = 3 + 0.14

Tuple
~~~~~~

.. code-block:: swift
    :linenos:

    let http404Error = (404, "Not Founbd")
    print("The status code is \(http404Error.0)")
    // or 
    let (statusCode, _) = (404, "Not Founbd")
    print("The status code is \(statusCode)")
    // or 
    let http404Error = (statusCode: 404, statusMessage: "Not Founbd")
    print("The status code is \(http404Error.statusCode)")

Optional (?)
~~~~~~~~~~~~~~~~~~

allowable nil

.. code-block:: swift
    :linenos:

    var name: String? = "Jack"
    name = nil

    var age: Int? //The default value is nil
    age = 10
    age = nil

.. code-block:: swift
    :linenos:

    var array = [1, 15, 40, 29]
    func get(_ index, Int) -> Int? {
        if index < 0 || index >= array.count {
            return nil
        }
        return array[index]
    }
    print(get(1)) // optional(15)
    print(get(-1)) // nil
    print(get(4)) // nil

Forced Unwrapping (!)
~~~~~~~~~~~~~~~~~~~~~~~~

``Int?`` as a box

.. code-block:: swift
    :linenos:

    var age: Int? = 10
    let ageInt: Int = age! // ageInt = 10
    ageInt += 10

.. code-block:: swift
    :linenos:

    var age: Int?
    age! // Fatal error... 

.. code-block:: swift
    :linenos:

    var num = Int("a123") // num.type is Int?

Optional Binding
~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:

    if let number = Int("123") {
        print("success \(number)")
    } else {
        print("fail")
    } // success 123

.. code-block:: swift
    :linenos:

    enum Season : Int {
        case spring = 1, summer, autumn, winter
    }
    if let season = Season(rawValue: 6) {
        switch season {
            case .spring:
                print("the season is spring")
            default:
                print("the season is other")
        }
    } else {
        print("no such season")
    } // no such season

.. code-block:: swift
    :linenos:

    if let first = Int("4") {
        if let second = Int("42") {
            if first < second && second < 100 {
                print("\(first) < \(second) < 100")
            }
        }
    }
    // is equivalence in
    if let first = Int("4"),
        if let second = Int("42"),
            first < second && second < 100 {
            print("\(first) < \(second) < 100")
    }

in while

.. code-block:: swift
    :linenos:

    var strs = ["10", "20", "abc", "-20", "30"]
    var index = 0
    var sum
    while let num = Int(strs[index]), num > 0 {
        sum += num
        index += 1
    }
    print(sum) //60

Nil-Coalescing Operator (??)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``A ?? B`` as ``Operator ?? Whatever``
if ``A`` is nil return ``A`` if ``A`` is not nil return ``B``, if ``B`` is not Operator return ``A``!


.. code-block:: swift
    :linenos:

    let a: Int? = 1
    let b: Int? = 2
    let c = a ?? b // c.type is Int?, Optional(1)


.. code-block:: swift
    :linenos:

    let a: Int? = nil
    let b: Int? = 2
    let c = a ?? b // c.type is Int?, Optional(2)


.. code-block:: swift
    :linenos:

    let a: Int? = nil
    let b: Int? = nil
    let c = a ?? b // c.type is Int?, nil


.. code-block:: swift
    :linenos:

    let a: Int? = 1
    let b: Int = 2
    let c = a ?? b // c.type is Int, 1


.. code-block:: swift
    :linenos:

    let a: Int? = nil
    let b: Int = 2
    let c = a ?? b // c.type is Int, 2

Source code


.. code-block:: swift
    :linenos:

    public func ?? <T>(optional: T?, defaultValue: @autoclosure () throws -> T?) rethrows -> T?
    public func ?? <T>(optional: T?, defaultValue: @autoclosure () throws -> T) rethrows -> T

Implicitly Unwrapped Optional
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

変数 ``Int!`` が常に値を持っていることを確認する必要があります。

.. code-block:: swift
    :linenos:

    let num1: Int! = 10
    let num2: Int = num1
    if num1 != nil {
        print(num1 + 6) // 16
    }
    if let num3 = num1 {
        print(num3)
    }

.. code-block:: swift
    :linenos:

    let num1: Int! = nil // Fatal error
    let num2: Int = num1


String Interpolation
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:

    var age: Int? = 10
    print("My age is \(age)") // error!!!
    // rewrite
    print("My age is \(age!)") // My age is 10
    print("My age is \(String(discribing: age))") // My age is Optional(10)
    print("My age is \(age ?? 0)") // My age is 10

Multiple Options
~~~~~~~~~~~~~~~~~~

.. code-block:: swift
    :linenos:

    var num1: Int? = 10
    var num2: Int?? = num1
    var num3: Int?? = 10
    num2 == num3 // ture












