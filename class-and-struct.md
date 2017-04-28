* ## Class

```
class Player {
    var name:String
    var age:Int
    let race = "Human"

    init (name:String, age:Int) {
        self.name = name
        self.age = age
    }

        // class function不能使用class內儲存屬性的property的值
        class func description(){
            print("This is a class for player!")
        }

        func showPlayerInfo() {
            print("\(self.name) is a \(self.age) \(self.race)")
        }
}
```

* #### 宣告instance

```
var playerOne = Player(name:"Kershaw", age:28)
var playerTwo = Player(name:"Harper", age:24)
let playerThree = Player(name:"Lily", age:20)


// 以後playerOne就等於playerThree
playerOne = playerThree
print("Player One is \(playerOne.name)")
## Player One is Lily

// 先印一次 playerTwo的年紀
print("Player Two is \(playerTwo.age) years old")
## Player Two is 24 years old

// 然後將playerTwo的記憶體位址指到playerOne，也就是playerThree的記憶體位址
playerTwo = playerOne
print("Player Two is \(playerTwo.age) years old")
## Player Two is 20 years old

// 在更改playerThree的年紀，即使是用let宣告，還是可以更改variable的值
playerThree.age = 100
print("Player Two is \(playerTwo.age) years old")
## Player Two is 100 years old

// 因為playerThree用let宣告，所以無法再更改記憶體位置
playerThree = playerOne
```

* ## Struct



