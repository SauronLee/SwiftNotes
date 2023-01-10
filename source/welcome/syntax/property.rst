プロパティ (Property)
==========


Stored Property
---------------

The essence is a member variable  
stored in instance memory  
|check| Struct (need initial value)
|check| Class (need initial value)
|uncheck| Enumerate


.. code-block:: swift
    :linenos:

    struct point {
        var x: Int
        var y: Int
        init() {
            x = 11
            y = 22
        }
    }


Computed Property
------------------

| The essence is the function  
| Not stored in instance memory  
| Only ``var`` can be used  

|check| Struct
|check| Class
|check| Enumerate


.. code-block:: swift
    :linenos:

    struct Circle {
        var radius: Double
        var diameter: Double {
            set(newDiameter) {
                radius = newDiameter / 2 //newValue
            }
            get {
                radius * 2
            }
        }
    }

Lazy Stored property

.. code-block:: swift
    :linenos:

    class Car{
        init() {
            print("Car init!")
        }
        func run() {
            print("Car is running!")
        }
    }
    class Person {
        lazy var car = Car()
        init() {
            print("Person init!")
        }
        func goOut() {
            car.run()
        }
    }
    // test
    let p = Person()
    // output: Person init!
    p.goOut()
    // output: 
    // Car init!
    // Car is running!

e.g.  

``lazy`` only ``var`` can be used

.. code-block:: swift
    :linenos:

    class PhotoView {
        lazy var image: Image = {
            let url = "https://www.xxx.com/xx.png"
            let data = Data(url: url)
            return Image(data: data)
        }()
    }


Property Observer
-------------------

.. code-block:: swift
    :linenos:

    struct Circle {
        var radius: Double {
            willSet {
                print("willSet", newValue)
            }
            didSet {
                print("didSet", oldValue, radius)
            }
        }
        init() {
            self.radius = 1.0
            print("Circle init!")
        }
    }
    // test
    var circle = Circle() // Circle init!
    circle.radius = 10.5 // willSet 10.5 \n didSet 1.0 10.5
    print(circle.radius) // 10.5


Inout
----------
The essence of inout is address passing.

.. code-block:: swift
    :linenos:

    struct Shape {
        var width: Int
        var side: Int {
            willSet {
                print("willSetSide", newValue)
            }
            didSet {
                print("didSetSide", oldValue, side)
            }
        }
        var girth: Int {
            set {
                width = newValue / side
                print("setGirth", newValue)
            }
            get {
                print("getGirth")
                return width * side
            }
        }
        func show() {
            print("width=\(width), side=\(side), girth=\(girth)")
        }
    }
    // test
    func test(_ num: inout Int) {
        num = 20
    }
    var s = Shape(width: 10, side: 4)
    test(&s.width)
    s.show()
    print("---")
    test(&s.side)
    s.show()
    print("---")
    test(&s.girth)
    s.show()
    /*
    getGirth
    width=20, side=4, girth=80
    ---
    willSetSide 20
    didSetSide 4 20
    getGirth
    width=20, side=20, girth=400
    ---
    getGirth
    setGirth 20
    getGirth
    width=1, side=20, girth=20
    */

Type Property 
--------------

* Instance Property
  
  * Stored Instance Property
  * Computed Instance Property
  
* Type Property
  
  * Stored Type Property
  * Computed Type Property


.. code-block:: swift
    :linenos:

    struct Car {
        static var count: Int = 0 // default `lazy` ; able to let or var
        init() {
            Car.count += 1
        }
    }
    // test
    let c1 = Car()
    let c2 = Car()
    let c3 = Car()
    print(Car.count) // 3

Singleton mode
---------------


.. code-block:: swift
    :linenos:

    public class FileManager {
        public static let shared = FileManager()
        private init() { }
    }
    // or
    public class FileManager {
        public static let shared = {
            // ...
            // ...
            return FileManager()
        }
        private init() { }
    }
