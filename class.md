# Class Diagram 
- 객체의 타입 표현
- 객체관의 관계 기술
- 설계 과정(협업) 에서 거의 필수적인 절차 

### 기본 형태 
```plantuml
@startuml

class Member{
    - id : String
    - name : String 
    - password : String 
    +changePassword(newPassword : String)
}
note top of Member: 클래스 이름 
note left of Member: 속성
note bottom of Member: 오퍼레이션(이름 : 리턴타입 )
@enduml
```

### 연관관계 나타내기 
대부분의 경우 1:n(n은 2 이상의 정수) 꼴로 나타남. 
따라서 1:n 형태로 많이 나타낸다. 
```plantuml 
@startuml
Class21 #-- Class22
Class23 x-- Class24
Class25 }-- Class26 
Class27 +-- Class28
Class29 ^-- Class30
@enduml
```


### Example 

1. BattleShip Game
```plantuml
@startuml
'''' Declarations for title, caption, etc ''''
'''' Declarations to stylize the diagram ''''
skinparam classFontStyle bold
skinparam classAttributeIconSize 0
'''' Attributes and methods '''
class BattleshipGame {
    - inputboard : ArrayList<ArrayList>
    <<constructor>> BattleshipGame()
    +playgame(board:board,player:player)
}
class Board {
    - virtualboard : ArrayList<ArrayList>
    - ships : ArrayList<ship>
    - traps : ArrayList<trap>
    - potions : ArrayList<potion>
    <<constructor>> Board(ship:int,trap:int,potion:int)
    +createboard() : ArrayList<ArrayList>
    +createships(num:int)
    +createtraps(num:int)
    +createpotions(num:int)
    +isoverlap(temp:potion) : boolean
    +getship() : ArrayList<ship>
    +gettrap() : ArrayList<trap>
    +getpotion() : ArrayList<potion>
    +getvirtualboard() : ArrayList<ArrayList>
    +displayboard(board : ArrayList<ArrayList>)
}
class Player {
    - live : int
    - steptaken : int
    - inputx : int
    - inputy : int
    - shipfound : int
    <<constructor>> Player()
    +getsteptaken() : int
    +addstep()
    +setlive(l:int)
    +getlive() : int
    +getshipfound() : int
    +setshipfound()
}
class Potion {
    - y : int
    - x : int
    - length : int
    - isused : boolean
    <<constructor>> Potion()
    +gety() : int
    +sety(y:int)
    +getx(i:int) : int
    +getlength() : int
    +isused() : boolean
    +setused()
}
class Ship {
    -posx : ArrayList<Object>
    -posy : int
    -length : int
    -sunken : boolean
    <<constructor>> Ship()
    +setposition(len:int)
    +setsunken()
    +getx(i:int) : int
    +gety() : int
    +getposx() : ArrayList<Object>
    +issunken() : boolean
    +getlength() : int
    +generateposition(x:int,y:int,len:int)
}
class Trap {
    - lives : int
    - y : int
    - x : int
    - reveal : boolean
    <<constructor>> Trap()
    +gety() : int
    +getx(i:int) : int
    +revealed()
    +isrevealed() : boolean
    +getlive() : int
    +getlength() : int
}
class ShipRevealPotion {
    <<constructor>> ShipRevealPotion()
    +revealship(temp:ArrayList<ship>, board:ArrayList<ArrayList>)
}
class LifeSaverPotion {
    <<constructor>> LifeSaverPotion()
    + reveal()
}
class TrapRevealPotion {
    <<constructor>> TrapRevealPotion()
    + revealtrap(temp:board, board:ArrayList<ArrayList>)
}
BattleshipGame "1" *-- "1" Board
BattleshipGame "1" *-- "1" Player
Board "1" *-- "20..80" Ship
Board "1"  *-- "10..30" Trap
Board "1"  *-- "0..18" Potion
Potion <|-- ShipRevealPotion
Potion <|-- LifeSaverPotion
Potion <|-- TrapRevealPotion
@enduml
```
2. Message
```plantuml 
@startuml

'Classes:
'-------------

class User {
  - id: int  
  - name: String  
  + sendMessage()  
  + addContact()
}

class Message {
  - id: int  
  - content: String
  + metadata: int
  + send()  

}

class Group {
  - id: int  
  - name: String
  + addMember() 
}


'Associations:
'-------------

"User" -- "Message"  
"User" -- "Group"

@enduml   
```