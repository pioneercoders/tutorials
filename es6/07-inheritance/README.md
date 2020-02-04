<h4> What is a Inheritance?</h4>
<p>One of the real benefits of object-oriented programming is the ability to build upon existing classes - to inherit all of the functionality of a well-written class and extend it for some purpose specific to your needs.</p>

```javscript
class Animal {
		constructor(name) {
			this.name = name;
			this.animaltype = 'animal';
		}
		toString() {
			return this.name + ' ' + this.animaltype;
		}
		speak() {
			return 'NA';
		}
	}

class Dog extends Animal {
		constructor(name) {
			super(name);
			this.animaltype = 'dog';
		}
		speak() {
			return 'woof';
		}
	}

var pet = new Animal('Cuddles');
console.log(pet.name + ' says "' + pet.speak() + '"');
	
var fido = new Dog('Fido');
console.log(fido.name + ' says "' + fido.speak() + '"');
```
