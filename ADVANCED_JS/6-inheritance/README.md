<h4> What is a Inheritance?</h4>
<p>One of the real benefits of object-oriented programming is the ability to build upon existing classes - to inherit all of the functionality of a well-written class and extend it for some purpose specific to your needs.</p>

<section>  
<div ui-ace ="{useWrapMode: 'true', showGutter : 'true', theme:'monokai', mode: 'html', previewId:'preview',
	onLoad: htmlcssjsContentOnLoaded,
	rendererOptions: { fontSize: 16 },
	advanced: { highlightActiveLine: true}
}" style="min-height:800px;"><xmp><html>
<head>
<script language="javascript" type="text/javascript">
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
		
</script>
</head>
<body><h3>Please open the console and see the log </h3>
	<h4 style="color:green;">Press Ctrl + Shift + J (Windows / Linux) or Cmd + Opt + J (Mac) to open console. </h4>
</body>
</html></xmp>
</div>
<div>
	<iframe id="preview"></iframe>
</div>
</section>
