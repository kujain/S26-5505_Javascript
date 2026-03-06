# Class 7 Exercises

### Class exercise: use above to get data from reqres and then format in the DOM.
```
let button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData() {

	const ul = document.createElement('ul');
	const url = 'https://reqres.in/api/users';
	const xhr = new XMLHttpRequest();
	xhr.onload = function() {
		if (xhr.status === 200  || xhr.status === 201) {

      // add your code here to process the response and format and add to the DOM
      
		}
	}
	xhr.open('GET', url, true);
  xhr.setRequestHeader( 'x-api-key', 'reqres-free-v1');
	xhr.send(null);
}
```

