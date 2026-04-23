#### SESSION #13

# JS FRAMEWORKS

## FRAMEWORKS

- Javascript development frameworks can help speed up coding and simplify the written code, especially for larger apps.
- The amount of code written is lesser since the framework handles many of the typical functionalities and takes care of many assumptions/decisions/defaults.
- They take care of many mundane tasks like updating the DOM in real-time.
- Also forces you to learn about latest coding practices and approaches since most frameworks enforce them.

## ANGULAR

- One of the most popular javascript frameworks.
- Built by google and available to anyone for free.
- Great for building complex web applications.
- Extends the HTML vocabulary by allowing attributes to be extended in the markup.
- Create and reuse components and use a wide array of existing ones.
- Uses a more sophisticated superset of javascript called typescript.
```
<input type="text" ng-model="yourName" placeholder="Enter a name here">
<h1>Hello {{yourName}}!</h1>

//--js
import { Component } from '@angular/core';
 
@Component({
  selector: 'my-app',
  template: `<h1>Hello {{name}}</h1>`
})
export class AppComponent { name = 'Angular'; }
```

## VUEJS

- Relatively simpler framework built for rapid prototyping for web and other applications.
- Built to be versatile and easy to implement.
- Good for building single page applications (SPA).
- Also allows building reusable components, templates, plugins etc.
- Uses MVVM pattern (Model-View-View Model):
```
<div id="app">
  {{ message }}
</div>

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```


## REACTJS

- Great for building complex interfaces using lots of dynamic data.
- Built by facebook and available as open-source.
- All html is written within a javascript file and format called JSX.
- Includes a bunch of other utilities and addons.
- Adopted by many new frameworks and libraries like Nextjs.
- A steep learning curve as best practices etc. take some practice.
- Versatile and can be used to develop web apps as well as mobile apps.
```
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}
```

## NEXTJS

- Backend/Front-end framework with features like server-side rendering, caching etc.
- Built on top of React and much faster.
- A more fully-loaded add-on for React - and considered to be the full-stack framework to use.
- Great for building sites that have both static pages (eg. homepages) and dynamic pages (eg. shopping carts, account pages etc.).



## OTHERS

- Backbone
- Ember
- Svelte
- Alpine
- Gatsby
- etc. etc.

https://ninetailed.io/blog/best-javascript-frameworks/
https://kinsta.com/blog/javascript-libraries/





## JSX WITH REACT

- React uses a mongrel syntax called JSX: JavaScript XML, to define the structure of the UI.
- Any JavaScript expressions can be inserted within braces inside JSX.
- Blurs the line between at least 2 traditional web components: html and js (somewhat breaks the 3 layers of web separation rule!) .

```
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <p>Instagram</p>
      </div>
    );
  }
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }

if (!recipe) {
    return <p>Recipe not found!</p>;
} else {
  	return (
    <div>
      <h1>{recipe.title}</h1>
      <p>{recipe.description}</h1>
    </div>
  );
}
```

## REACT COMPONENTS

- In React all code is structured around Components. 
- Everything that can interact in a React application is a component
- The main Component (root) is called App.
- Allows for encapsulating different parts of the UI into independent, reusable pieces.
- Functional components are equivalent to standard js functions: do not hold any internal state
- Class components are equivalent to standard class js structure: more complex and can hold/store internal state

eg. of Functional:
```
function UserProfile(props) {
  return (
    <div className="user-profile">
      <img src={props.userProfile.picture} />
      <p>{props.userProfile.name}</p>
    </div>
  );
}
```

eg. of Class Component: 
```
class SubscriptionForm extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      acceptedTerms: false,
      email: '',
    };
  }

  updateCheckbox(checked) {
    this.setState({
      acceptedTerms: checked,
    });
  }

  submit() {
    // ... use email and acceptedTerms in an ajax request...
  }

  render() {
    return (
      <form>
        <input
          type="email"
          onChange={(event) => {this.updateEmail(event.target.value)}}
          value={this.state.email}
        />
        <input
            type="checkbox"
            checked={this.state.acceptedTerms}
            onChange={(event) => {this.updateCheckbox(event.target.checked)}}
          />
        <button onClick={() => {this.submit()}}>Submit</button>
      </form>
    )
  }
}
```

## RENDERING

React renders components on the fly (no user reload necessary) when its props or state changes
```
// call to this will trigger a re-render
this.setState({
  user.name: 'Rachel',
});
```

props change:
```
import React from 'react';
import UserProfile from './UserProfile';

class App extends () {
  constructor(props) {
    super(props);
    this.state = {
      user: {
        name: 'Jane Doe',
        picture: 'https://cdn.google.com/picture/jane.png',
      },
    };
  }

  render() {
    return (
      <div>
       **<UserProfile userProfile={this.state.user} />**
      </div>
    );
  }
}
```

## ROUTING

- React Router is a collection of navigational components that allow create virtual paths for the application
- Great for creating SPA (Single Page Applications) but still allow generated urls/navigation for content without page reloads (good for SEO)
- Allows for a more seamless web user experience - emulates an application 

```
npm install react-router-dom
```

```
import { BrowserRouter as Router} from ‘react-router-dom’

ReactDOM.render(
  <Router>
    <App />
  </Router>
, document.getElementById('root'));
```



## EXAMPLE APP: Class Roster application

- Build a Class Student Roster using React 
- Will use Node/Express Backend 
- JSON file-based database
- Will use React components and Routers
- Uses JSON file as a DB but can be modified in backend code to use MondoDB instead

Download the reference files here: https://github.com/kujain/S26-5505_Javascript/blob/main/class-roster-2026-boileterplate-files.zip

Use code from here:[[[https://github.com/kujain/S23-5505_Javascript/blob/main/Class%2013%20Notes.md]([https://github.com/kujain/S26-5505_Javascript/blob/main/class%2013%20notes.md](https://github.com/kujain/S26-5505_Javascript/blob/main/class%2013%20notes.md))](https://github.com/kujain/F25-5505_Javascript/blob/main/class%2013%20notes.md)](https://github.com/kujain/S26-5505_Javascript/blob/main/class%2013%20notes.md)


## BACKEND

```
$ mkdir class-roster
$ cd class-roster/
$ mkdir backend
$ cd backend/
$ npm init -y
$ npm i body-parser cors express helmet morgan
$ code index.js
```

- Replace backend/index.js with code from Boilerplate
- Copy data/courses.json into backend folder
- edit package.json:

```
  "start": "node index.js"
```

- Start node:
```
$ npm start
```

- Use Postman app to test the API (course, student etc.).






## REACT - 1

- In a new terminal window, initialize React:
```
$ cd class-roster/
$ npx create-react-app frontend
$ cd frontend/
```

**Note:** current react version is v18. but this app is in v17 so some downgrading changes are needed first:
- delete node-modules and package-lock.json files
- Run:
```
npm install react@17.0.2 react-dom@17.0.2
npm install @testing-library/react@12.1.5
npm install @testing-library/react@12.1.5
```
- In a new terminal window, initialize React:
```
// for development
$ npm start

//to build final production files
$ npm run-script build 
```

- Install additional packages:
```
$ npm i react-router@5.1.2 react-router-dom@5.1.2
```

- Initial code:
```
// replace src/App.js and src/index.js with code from Boilerplate: 
$ npm start
```


## REACT - 2

- setup bootstrap and basic css in public/index.html and index.css
```
<link rel="stylesheet" href="https://bootswatch.com/4/lux/bootstrap.min.css">
<title>Class Roster App</title>
```
```
body {
  margin: 100px 25px;
}
```

- setup React Navbar component: copy code from NavBar/NavBar.js 
- Update App.js and add

```
import NavBar from './NavBar/NavBar';
…
    return (
      <div>
        **<NavBar/>**
        <p>Work in progress.</p>
      </div>
    );
```







## REACT - 3

- Building Class Components for handling the Courses:
- Stop npm and Install axios:
```
npm i axios
```
- Create Courses/Courses.js and add code from the boilerplate
- Update app.js:

```
import Courses from './Courses/Courses';
…
  render() {
    return (
      <div>
        <NavBar/>
        **<Courses/>**
      </div>
    );
  }
```

- Restart npm:
```
npm start
```



## REACT - 4

- Setup a route to view details on a Course:
- Create Course/Course.js component and add code from the boilerplate (use course_0.js for the code)
- Update app.js:
```
import {Route} from 'react-router-dom';
...
**import Course from './Course/Course';**


…
  render() {
    return (
      <div>
        <NavBar/>
        **<Route exact path='/' component={Courses}/>
        <Route exact path='/course/:courseId' component={Course}/>**
      </div>
    );
  }
```



## REACT - 5

- Setup a component to add a new Course:
- Create NewCourse/NewCourse.js component and add code from the boilerplate
- Update app.js:

```
import NewCourse from './NewCourse/NewCourse';
…
  render() {
    return (
      <div>
        <NavBar/>
        <!-- ...navbar and other routes... -->
        **<Route path='/new-course' component={NewCourse} />**


      </div>
    );
  }
```

- Update Courses.js:
```
**<div className="col-sm-12 col-md-4 col-lg-3">
 <Link to="/new-course">
    <div className="card bg-primary mb-3 text-white">
      <div className="card-header">Need help? Ask here!</div>
      <div className="card-body">
        <h4 className="card-title">+ Add a Course</h4>
        <p className="card-text">Don't worry. Help is on the way!</p>
      </div>
    </div>
  </Link>
</div>**
…
{this.state.courses === null && <p>Loading Courses...</p>}

```





## REACT - 6

- Setup a component to add new students:
- Create Course/AddStudent.js component and add code from the boilerplate AddStudent.js
- Update Course.js from the boilerplate Course.js and then add below to the file:

```
**import AddStudent from './AddStudent';**
…

  **async submitStudent(student) {
    await axios.post(`http://localhost:8000/student/${this.state.course.id}`, {
      name: student,
    });
    await this.refreshCourse();
  }**
		. . .
  render() {
    return (
		. . .
         <hr className="my-4" />
         **<AddStudent courseId={course.id} submitStudent={this.submitStudent} />**
         <p>Students:</p>
		. . .

      </div>
    );
  }
```
- Test and verify in the backend database as well.





## NEXTJS - Sample async app

- NEXTJS provides a way to handle both frontend and backend (server) rendering
- Create a new nextjs app:

```
mkdir test-project1
npm i -g create-next-app
npx create-next-app@14 test-project1
(no tailwind, no Eslint, yes src, no import alias, no App Router, no typescript)
cd test-project1
npm run dev
```

- Run > http://localhost:3000/








## NEXTJS - 2

- Add Static Rendering: this data doesnt change often
- Update Index.js:
```
export default class extends Component {
  render () {
    return (
      <div>
        <div>{this.props.title}</div>
        <div><img src={this.props.imageUrl} /></div>
      </div>
    )
  }
}

export async function getStaticProps() {
  const res = await fetch(
    "https://api.nasa.gov/planetary/apod?api_key=GTa94pq1MZEXiPDmLS4n1CSqIJxRkQLI9MCjOqa4"
  );
  const data = await res.json();

  return {
    props: {
      title: data.title,
      imageUrl: data.url,
    },
  };
}
```





## NEXTJS - 3

- Add Additional pages
- Use getServerSideProps: this is loaded on each page during load/runtime
- Create src/pages/posts/index.js:

```
import Head from "next/head";
import { Inter } from "next/font/google";
import styles from "@/styles/Home.module.css";
import React, { Component } from 'react';
import Link from 'next/link';

const inter = Inter({ subsets: ['latin'] });


export default function index({ data }) {
  return (
    <main className={`${styles.main} ${inter.className}`}>
    <div>
      <h2>Posts API</h2>
      <ul>
        {data.map((post) => {
          return <li key={post.id}>
            <p><Link href={`/posts/${post.id}`} className={styles.vercelLogo}>
              {post.first_name} {post.last_name}
            </Link></p></li>;
        })}
      </ul>
    </div>
      </main>
  );
}

export async function getServerSideProps() {
  const res = await fetch(
    `https://reqres.in/api/users`,
    {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
        'x-api-key': 'reqres-free-v1'
      }
    }
  );
  const posts = await res.json();
  const data = posts.data;
  return { props: { data } };
}
```
