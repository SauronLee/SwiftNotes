クロージャ (Closure)
------------------------


.. code-block:: swift
    :linenos:
    
    typelias Fn = (Int) -> Int
    func getFn() -> Fn {
        var num = 0
        func plus(_ i: Int) -> Int{
            num += i
            return num
        }
        return plus
    }
    // by closure expression
    func getFn() -> Fn{
        var num = 0
        return {
            num += $0
            return num
        }
    }
    // instance
    var fn1 = getFn()
    var fn2 = getFn()
    fn1(1) // 1
    fn2(2) // 2
    fn1(3) // 4
    fn2(4) // 6
    fn1(5) // 9
    fn2(6) // 12

Closure as a Class instance
----------------------------

.. code-block:: swift
    :linenos:
    
    class Closure {
        var num = 0
        func plus(_ i: Int) -> Int {
            num += i
            return num
        }
    }
    // instance
    var cs1 = Closure()
    var cs2 = Closure()
    cs1(1) // 1
    cs2(2) // 2
    cs1(3) // 4
    cs2(4) // 6
    cs1(5) // 9
    cs2(6) // 12

Class
------

.. code-block:: swift
    :linenos:
    
    class Closure {
        i: Int
        init(_ i: Int) {
            self.i = i
        }
        func get() -> Int {
            return i
        }
    }
    var class: [Closure] = []
    for i in 1...3 {
        class.append(Closure(i))
    }
    for cls in class {
        print(cls.get())
    }

Autoclosure
------------

.. code-block:: swift
    :linenos:
    
    func getFirstPositive(_ v1: Int, _ v2: Int) -> Int {
        return v1 > 0 ? v1 : v2
    }
    getFirstPositive(10, 20) // 10
    getFirstPositive(-2, 20) // 20
    getFirstPositive(0, -4) // -4
    ```
    Let v2 delay loading (rewrite by function type)
    ```swift
    func getFirstPositive(_ v1: Int, _ v2: () -> Int) -> Int {
        return v1 > 0 ? v1 : v2()
    }
    getFirstPositive(-4) { 20 }
    // as
    func getFirstPositive(_ v1: Int, _ v2: @autoclosure () -> Int) -> Int {
        return v1 > 0 ? v1 : v2()
    }
    getFirstPositive(-4, 20)
