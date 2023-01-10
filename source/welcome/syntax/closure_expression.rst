クロージャ式 (Closure Expression)
================================

.. code-block:: swift
    :linenos:
    
    func sum(_ v1: Int, _ v2: Int) -> Int {v1 + v2}
    // ==
    var fn = {
        (v1: Int, v2: Int) -> Int in return v1 + v2
    }
    fn(10, 20)
    // == 
    {
        (v1: Int, v2: Int) -> Int in return v1 + v2
    }(10, 20) // anonymous function

Shorthand for Closure Expressions

.. code-block:: swift
    :linenos:
    
    func exec(v1: Int, v2: Int, fn: (Int, Int) -> Int) {
        print(fn(v1, v2))
    }
    // Instance
    exec(v1: 10, v2: 20, fn: {
        (v1: Int, v2: Int) -> Int in return v1 + v2
    })
    // ==
    exec(v1: 10, v2: 20, fn: {
        v1, v2 in return v1 + v2
    })
    // ==
    exec(v1: 10, v2: 20, fn: {
        v1, v2 in v1 + v2
    })
    // ==
    exec(v1: 10, v2: 20, fn: {$0 + $1})
    // ==
    exec(v1: 10, v2: 20, fn: + })

Trailing Closure
------------------

if it is the last parameter

.. code-block:: swift
    :linenos:
    
    func exec(v1: Int, v2: Int, fn: (Int, Int) -> Int) {
        print(fn(v1, v2))
    }
    // can be as
    exec(v1: 10, v2: 20){$0 + $1}

If only one parameter

.. code-block:: swift
    :linenos:
    
    func exec(fn: (Int, Int) -> Int) {
        print(fn(1, 2))
    }
    // can be as
    exec(fn: {$0 + $1})
    // ==
    exec() {$0 + $1}
    // ==
    exec {$0 + $1}
