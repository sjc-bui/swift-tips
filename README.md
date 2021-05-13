## #1 `UITableViewCell` identifier

```swift
extension UITableViewCell {
    static var identifier: String {
        return String(describing: self)
    }
}

let cell = tableView.dequeueReusableCell(withIdentifier: TableViewCell.identifier)
tableView.register(TableViewCell.self, forCellReuseIdentifier: TableViewCell.identifier)

print(TableViewCell.identifier) //TableViewCell
```


## #2 Enumerated interation

```swift
for (i, v) in "Swift Programming Language".enumerated() {
    print("Index: \(i), Value\(v)")
}
```

## #3 Remove element from `Array`
```swift
extension Array where Element: Equatable {
    mutating func remove(_ object: Element) {
        if let index = self.firstIndex(of: object) {
            remove(at: index)
        }
    }
}
```

## #4 Group objects by property
```swift
extension Sequence {
    func group<GroupingType: Hashable>(by key: (Iterator.Element) -> GroupingType) -> [[Iterator.Element]] {
        var groups: [GroupingType: [Iterator.Element]] = [:]
        var groupsOrder: [GroupingType] = []
        forEach { element in
            let key = key(element)
            if case nil = groups[key]?.append(element) {
                groups[key] = [element]
                groupsOrder.append(key)
            }
        }
        return groupsOrder.map { groups[$0]! }
    }
}
```

Usage:
```swift
struct Person {
    var name: String
    var age: Int
}

let mike = Person(name: "Mike", age: 18)
let john = Person(name: "John", age: 18)
let bob = Person(name: "Bob", age: 56)
let jake = Person(name: "Jake", age: 56)
let roman = Person(name: "Roman", age: 25)

let persons = [mike, john, bob, jake, roman]

let groupedPersons = persons.group { $0.age }

for persons in groupedPersons {
    print(persons.map { $0.name })
}
```
Result:
```swift
["Mike", "John"]
["Bob", "Jake"]
["Roman"]
```
