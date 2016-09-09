var parent = {money: 100}
var child = Object.create(parent) // prototype link between child and parent

child.money => 100
parent.money = 200
child.money => 200
child.hasOwnProperty => false

prototype link VS prototype chain (link)
