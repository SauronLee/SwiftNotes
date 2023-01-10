数え上げ (Enumerate)
====================

Defination

.. code-block:: swift
    :linenos:
    
    enum Direction {
        case north
        case south
        case east
        case west
    }
    // or
    enum Direction {
        case north,south,east,west
    }
    // new
    var dir = Direction.west
    dir = Direction.east
    dir = .north
    print(dir) // north

Associated values
-------------------

.. code-block:: swift
    :linenos:
    
    enum Score {
        case points(Int)
        case grade(Character)
    }
    var score = Score.points(96)
    score = .grade("A")


.. code-block:: swift
    :linenos:
    
    enum Date {
        case digit(year: Int, month: Int, day: Int)
        case string(String)
    }
    var date = Date.digit(year: 2023, month: 1, day: 2)
    date = .string("2023-01-02")
    switch date {
        case .digit(let year, let month, let day):
            print(year, month, day)
        case let .string(value):
            print(calue)
    }

Raw Value
------------

.. code-block:: swift
    :linenos:
    
    enum PokerSuit : Character {
        case spade = "♠️"
        case heart = "♥️"
        case diamond = "♦️"
        case club = "♣️"
    }

    var suit = PokerSuit.spade
    print(suit) // spade
    print(suit.rawValue) // ♠️
    print(PokerSuit.club.rawValue) // ♣️


.. code-block:: swift
    :linenos:
    
    enum Grade : String {
        case perfect = "A"
        case great = "B"
        case good = "C"
        case bad = "D"
    }

    print(Grade.perfect.rawValue) // A
    print(Grade.great.rawValue) // B
    print(Grade.good.rawValue) // C
    print(Grade.bad.rawValue) // D

Implicitly Assigned Raw Value
------------------------------

.. code-block:: swift
    :linenos:
    
    enum Direction : String {
        case north = "north"
        case south = "south"
        case east = "east"
        case west = "west"
    }
    // equivalence in
    enum Direction : String {
        case north, south, east, west
    }
    print(Direction.north) //north
    print(Direction.north.rawValue) //north


.. code-block:: swift
    :linenos:
    
    enum Direction : Int {
        case north, south, east, west
    }
    print(Direction.north) //north
    print(Direction.north.rawValue) //north


.. code-block:: swift
    :linenos:
    
    enum Season : Int {
        case spring = 1, summer, autumn = 4, winter
    }
    print(Season.spring.rawValue) // 1
    print(Season.summer.rawValue) // 2
    print(Season.autumn.rawValue) // 3
    print(Season.winter.rawValue) // 4

Recursive Enumeration
----------------------

.. code-block:: swift
    :linenos:
    
    indirect enum ArithExpr {
        case number(Int)
        case sum(ArithExpr, ArithExpr)
        case difference(ArithExpr, ArithExpr)
    }
    // or
    enum ArithExpr {
        case number(Int)
        indirect case sum(ArithExpr, ArithExpr)
        indirect case difference(ArithExpr, ArithExpr)
    }


.. code-block:: swift
    :linenos:
    
    let five = ArithExpr.number(5)
    let four = ArithExpr.number(4)
    let two = ArithExpr.number(2)
    let sum = ArithExpr.sum(five, four)
    let difference = ArithExpr.difference(sum, two)

    func calculate(_ expr: ArithExpr) -> Int {
        switch expr {
            case let .number(value):
                return value
            case let .sum(left, right):
                return calculate(left) + calculate(right)
            case let .difference(left, right):
                return calculate(left) - calculate(right)
        }
    }
    calculate(difference)

