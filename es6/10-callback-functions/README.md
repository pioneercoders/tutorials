<h4> What is Callback Functions? </h4>
<p>In Javascript we can pass a function to another function as parameter, calling that parameter function, we called as callback function. </p>

```javascript
var success = function(){
	console.log("getcities success show results to user ...");
	}
	
var failure = function(){
	console.log("getcities failed show error msg to user...");
	}
	
var getCities = function(successCallback,failureCallback) {
		//getcities from db. 
		var isCitiesAvaliable = true;
		if(isCitiesAvaliable){
			successCallback();
		}else{
			failureCallback();
		}
	}
	
getCities(success,failure);

```

```html
<iframe id="preview"></iframe>
```

<p>In above example, success and failure are the functions which passed as parameter to getCities function. On succesfull retrival of the cities wer are calling successCallback and if any failure we are calling failureCallback functions. </p>
