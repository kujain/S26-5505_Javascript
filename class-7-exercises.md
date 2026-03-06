# Class 7 Exercises

### Class exercise: use above to get data from reqres and then format in the DOM.
```
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData() {

	const url = 'https://reqres.in/api/users';
	fetch(
    url,
		{
			method: 'GET',
			headers: {
        		'x-api-key': 'reqres_95b045da93704c77a365da5f0df9ef90'
      		},
		})
		.then(function(response) {
			return response.json();
		})
		.then(function(resp) {
			document.getElementById("Output").innerHTML = JSON.stringify(resp.results[0]);

      // add your code here to process the response and format and add to the DOM

    })
		.catch(function(error) {
			document.getElementById("Output").innerHTML = "There was an error "+error;
		});

}

```

