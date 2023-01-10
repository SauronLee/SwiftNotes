テンプレート
============

User Login
-----------

.. code-block:: swift
    :linenos:

    func login(_ info: [String : String]) {
        let username: String
        if  let tmp = info["username"] {
            username = tmp
        } else {
            print("enter your name")
            return
        }
        let password: String
        if  let tmp = info["password"] {
            password = tmp
        } else {
            print("enter your password")
            return
        }
        // if username
        // if password
        print("username: \(username)", "password: \(password)")
    }
    login(["username": "jack", "password": "123456"]) // username: jack password: 123456
    login(["password": "123456"]) // enter your name
    login(["username": "jack"]) // enter your password

or

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

Photo Loading
---------------

.. code-block:: swift
    :linenos:

    class PhotoView {
        lazy var image: Image = {
            let url = "https://www.xxx.com/xx.png"
            let data = Data(url: url)
            return Image(data: data)
        }()
    }
