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
			document.getElementById("Output").innerHTML = JSON.stringify(resp.data);

	      // add your code here to process the response and format and add to the DOM

    })
		.catch(function(error) {
			document.getElementById("Output").innerHTML = "There was an error "+error;
		});

}

```

Using XMLttpRequest:
```
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData() {
  let button = document.getElementById('GetUsers');
  button.addEventListener("click", getUserData);
  
  function getUserData() {
  
    const ul = document.createElement('ul');
    const url = 'https://reqres.in/api/users';
    const xhr = new XMLHttpRequest();
    xhr.onload = function() {
      if (xhr.status === 200  || xhr.status === 201) {
        let authors = JSON.parse(xhr.responseText); // Get results
        console.log(authors)
        for (key in authors.data) { // loop through the results
          let author = authors.data[key]; //assign current row to author var
          let li = document.createElement('li'), //  Create the elements we need
              img = document.createElement('img'),
              span = document.createElement('span');
          img.src = author.avatar;  // Add the source of the image to be the src of the img element
          span.innerHTML = author.first_name + ' ' +author.last_name; // Make the HTML of our span to be the first and last name of our author
          li.appendChild(img); // Append img element back tocontaining li
          li.appendChild(span); // Append span element back tocontaining li
          ul.appendChild(li); // Append li element back tocontaining ul
        }
        const sect = document.getElementsByTagName("section")[0];
        sect.append(ul); //Append the new ul to body
      }
    }
    xhr.open('GET', url, true);
    xhr.setRequestHeader( 'x-api-key', 'reqres_95b045da93704c77a365da5f0df9ef90');
    xhr.send(null);
  }
}
```

Using Promise:
```
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData(e) {
  e.preventDefault();

  const url = 'https://reqres.in/api/users';
  const ul = document.createElement('ul');

  const xhr = new Promise( function(resolve, reject) {
    const xhr = new XMLHttpRequest();
    xhr.open( 'GET', url, true );
    xhr.setRequestHeader( 'x-api-key', 'reqres_95b045da93704c77a365da5f0df9ef90');
    xhr.send();

    xhr.onload = function () {
      if (xhr.status === 200) {
          console.log(url);
          const response = JSON.parse(xhr.responseText);
          resolve(response);
      } else {
          const error = xhr.statusText || 'The reason is mysterious. Call Yoda!';
          reject(error);
      }
    }
  });

	xhr
		.then(function(resp) {
			let authors = resp; // Get results
			for (key in authors.data) { // loop through the results
				let author = authors.data[key]; //assign current row to author var
				let li = document.createElement('li'), //  Create the elements we need
						img = document.createElement('img'),
						span = document.createElement('span');
				img.src = author.avatar;  // Add the source of the image to be the src of the img element
				span.innerHTML = author.first_name + ' ' +author.last_name; // Make the HTML of our span to be the first and last name of our author
				li.appendChild(img); // Append img element back tocontaining li
				li.appendChild(span); // Append span element back tocontaining li
				ul.appendChild(li); // Append li element back tocontaining ul
			}
      		const sect = document.getElementsByTagName("section")[0];
			sect.append(ul); //Append the new ul to body

		})
		.catch(function(error){
			document.getElementById("Output").innerHTML = "There was an error in the api: " + error;
		});
}
```

Using Fetch:
```
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData(e) {
  e.preventDefault();

  const url = 'https://reqres.in/api/users';
  const ul = document.createElement('ul');

  fetch(
    url,
    {
      method: 'GET',
      headers: {
        'x-api-key': 'reqres_95b045da93704c77a365da5f0df9ef90'
      }
    }
  )
    .then(function(response) {
        return response.json();
    })
    .then( function(data) {

        let authors = data.data; // Getresults
        for (author of authors) { // loop through theresults
            console.log('raw data',author);
            let li = document.createElement('li'); //  Create theelements we need
            let img = document.createElement('img');
            let span = document.createElement('span');

            img.src = author.avatar;  // Add the source ofthe image to be the src of the img element
            span.innerHTML = author.first_name + ' ' +author.last_name; // Make the HTML of our span to be the firstand last name of our author
            li.appendChild(img); // Append img element back tocontaining li
            li.appendChild(span); // Append span element back tocontaining li
            ul.appendChild(li); // Append li element back tocontaining ul

            const sect = document.getElementsByTagName("section")[0];
            sect.append(ul); //Append the new ul to section
        }

    } )
    .catch(function(error) {
        document.getElementById("Output").innerHTML = "There was an error "+error;
    });
}
```
Using Async/Await:
```
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

async function getUserData(e) {
  e.preventDefault();

  const url = 'https://reqres.in/api/users';
  const ul = document.createElement('ul');

  const xhr = new Promise( function(resolve, reject) {
    const xhr = new XMLHttpRequest();
    xhr.open( 'GET', url, true );
    xhr.setRequestHeader( 'x-api-key', 'reqres_95b045da93704c77a365da5f0df9ef90');
    xhr.send();

    xhr.onload = function () {
      if (xhr.status === 200) {
          console.log(url);
          const response = JSON.parse(xhr.responseText);
          resolve(response);
      } else {
          const error = xhr.statusText || 'The reason is mysterious. Call Yoda!';
          reject(error);
      }
    }
  });

  const resp = await xhr;

  let authors = resp; // Get results
  for (key in authors.data) { // loop through the results
    let author = authors.data[key]; //assign current row to author var
    let li = document.createElement('li'), //  Create the elements we need
        img = document.createElement('img'),
        span = document.createElement('span');
    img.src = author.avatar;  // Add the source of the image to be the src of the img element
    span.innerHTML = author.first_name + ' ' +author.last_name; // Make the HTML of our span to be the first and last name of our author
    li.appendChild(img); // Append img element back tocontaining li
    li.appendChild(span); // Append span element back tocontaining li
    ul.appendChild(li); // Append li element back tocontaining ul
  }
  const sect = document.getElementsByTagName("section")[0];
  sect.append(ul); //Append the new ul to body
}

```

### AI Example:
```
// fetch get
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);


// OPEN AI:
function getUserData(e) {
    e.preventDefault();
    // start the form event handler on submit
    console.log('sending to OPEN AI');
    // get the prompt value
    const prompt = document.getElementById('aiQ').value;

    // build the generator params
    let json = JSON.stringify({
        "model": "gpt-3.5-turbo",
        "messages": [
          {
            "role": "user",
            "content": "Hello!"
          },
          {
            "role": "user",
            "content": prompt,
          }
        ]
    });
    // sorry I cannot share my api key here, as GIthub will delete it to avoid possible exposure. So you will need to generate your own and use here to run this test:
    const apiKey = 'sk-proj-***';

    fetch( `https://api.openai.com/v1/chat/completions`,
        {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                Accept: 'application/json',
                authorization: `Bearer ${apiKey}`,
            },
            body: json,
        })
        .then(response => response.json())
        .then(json => {
            // once received, assign to img element and render
            console.log(json);

            const message = json.choices[0].message.content.replace(/\n/g, "<br />");

            document.getElementById("Output").innerHTML += `<br> ${message}`;

        });
}
```

### Example of Chaining Ajax requests using Fetch:
```
function getUserData(e) {
  e.preventDefault();

  const url = "https://randomuser.me/api/?results=1";
  const url2 = "http://api.open-notify.org/iss-now.json";
  let coords; // this is needed still.

  fetch(url)
    .then(function(response) {
        return response.json();
    })
    .then( function(data) {
        console.log('raw data',data);
        document.getElementById("Output").innerHTML = JSON.stringify(data.results[0]);
        coords = data.results[0].location.coordinates;

       return fetch(url2);
    } )
    .then( function(response) {
        return response.json();
    })
    .then(function(resp) {
        console.log('raw data',resp);
        let iss = resp.iss_position;
        document.getElementById("Output").innerHTML += `<br>ISS position is: ${iss.latitude} / ${iss.longitude}`;
        let dist = distance( coords.latitude, coords.longitude, iss.latitude, iss.longitude);
        document.getElementById("Output").innerHTML += `<br>Current distance between the two  is: ${dist} miles`;
    })
    .catch(function(error) {
        document.getElementById("Output").innerHTML = "There was an error "+error;
    });
}

// distance function: helper function for iss distance calculation
function distance(lat1, lon1, lat2, lon2, unit) {
	if ((lat1 == lat2) && (lon1 == lon2)) {
		return 0;
	}
	else {
		let radlat1 = Math.PI * lat1/180;
		let radlat2 = Math.PI * lat2/180;
		let theta = lon1-lon2;
		let radtheta = Math.PI * theta/180;
		let dist = Math.sin(radlat1) * Math.sin(radlat2) + Math.cos(radlat1) * Math.cos(radlat2) * Math.cos(radtheta);
		if (dist > 1) {
			dist = 1;
		}
		dist = Math.acos(dist);
		dist = dist * 180/Math.PI;
		dist = dist * 60 * 1.1515;
		if (unit=="K") { dist = dist * 1.609344 }
		if (unit=="N") { dist = dist * 0.8684 }
		return dist;
	}
}
```
