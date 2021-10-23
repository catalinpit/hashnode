## Search and Filter Data in React Using Hooks

Searching and filtering data is a common feature in all applications. The users should be able to search for specific things when using an application.

In my case, I had to implement this feature recently in a simple React application, and I thought of sharing my solution with you.

## Context

Before going further, I want to provide some context. Let's consider you have a simple phonebook, where you store people and their phone numbers. 

The array of objects below represents the phonebook.

```javascript
const people = [
  { name: 'Alan Turing', number: '040-123456', id: 1 },
  { name: 'Ada Lovelace', number: '39-44-5323523', id: 2 },
  { name: 'Barbara Liskov', number: '12-43-234345', id: 3 },
  { name: 'Mary Poppendieck', number: '39-23-6423122', id: 4 }
]
```

So, the users should be able to search and filter people by their names. With that cleared, let's start building the solution!

## Search and filter data

For this article, you can create a standard React application using the following command:

```javascript
npx create-react-app phonebook
```

You only need `App.js` and `index.js`, so you can remove the other files such as CSS and test files.

### Application skeleton

Let's start by creating the skeleton of the application. Open the `App.js` file and write the following code:

```javascript
import React, { useState } from "react";

const App = (props) => {
  return (
    <>
      <h2>Phone book</h2>
      <input type="text" />
      <h2>Numbers</h2>
    </>
  );
};

export default App;
```

At this point, the application display three things on the page:
* the heading "Phone book"
* an input field
* the heading "Numbers"

Even though the input field is there, it does not do anything yet.

### Add state

The next step is to add state to the application. We add state to a React application by using the state hook - `useState`.

Write the following code in the file `App.js`:

```javascript
import React, { useState } from "react";

const App = (props) => {
  const people = [
    { name: "Alan Turing", number: "040-123456", id: 1 },
    { name: "Ada Lovelace", number: "39-44-5323523", id: 2 },
    { name: "Barbara Liskov", number: "12-43-234345", id: 3 },
    { name: "Mary Poppendieck", number: "39-23-6423122", id: 4 }
  ];

  const [persons, setPersons] = useState(people);
  const [search, setNewSearch] = useState("");

  return (
    <>
      <h2>Phone book</h2>
      <input type="text" />
      <h2>Numbers</h2>
    </>
  );
};

export default App;
```

There are three additions:
1. You imported the array of people at the top of the component. You store the data as an array in the component itself for this application because it is a simple app.
2. The `persons` variable is assigned the array of people as the initial state.
3. The `search` variable is assigned an empty string as the initial state. You will use the function `setNewSearch` to modify the state of the `search` variable.

The next step is to handle the searching functionality.

### Handle searching

When the user types something in the input field, the state of the `search` constant should also be updated.

For instance, if the user types "Alan" in the input field, the `search` state should be "Alan" too.

Thus, just after declaring the state variables, write the following function:

```javascript
const handleSearchChange = (e) => {
    setNewSearch(e.target.value);
};
```

This `handleSearchChange` function gets called every time the input field changes, and it sets the `search` state to the data from the input field.

Also, update the input element to look as follows:

```javascript
<input type="text" value={search} onChange={handleSearchChange} />
```

Now, you registered an event handler to the input's `onchange` attribute. The function `handleSearchChange` fires as soon as the input's value changes.

```javascript
import React, { useState } from "react";

const App = (props) => {
  const people = [
    { name: "Alan Turing", number: "040-123456", id: 1 },
    { name: "Ada Lovelace", number: "39-44-5323523", id: 2 },
    { name: "Barbara Liskov", number: "12-43-234345", id: 3 },
    { name: "Mary Poppendieck", number: "39-23-6423122", id: 4 }
  ];

  const [persons, setPersons] = useState(props.people);
  const [search, setNewSearch] = useState("");

  const handleSearchChange = (e) => {
    setNewSearch(e.target.value);
  };

  return (
    <>
      <h2>Phone book</h2>
      Filter persons:{" "}
      <input type="text" value={search} onChange={handleSearchChange} />
      <h2>Numbers</h2>
    </>
  );
};

export default App;
```

The next step is to use the `search` to filter the array of people and only display the ones matching the search data.

### Filtering the data

The logic for filtering is as follows:
* if the users did not search for anything, display the whole array of people
* if the users entered data, return only those people whose name contains the entered data

Write the following piece of code after the `handleSearchChange` function:

```javascript
const filtered = !search
    ? people
    : people.filter((person) =>
        person.name.toLowerCase().includes(search.toLowerCase())
      );
```

In the above code, you use the conditional ternary operator to decide what to return. `!search` returns "true" if the input field is empty and returns "false" otherwise.

If the users do not type anything in the search box, the function returns all the people. On the other hand, if the user searches for a person, the function returns only the people whose name includes the search term.

For example, if you type "lac" in the search box, the function `filtered` only returns "Ada Lovelace" because that is the only person whose name contains the search term "lac".

The `filter` method creates a new array with all the elements that pass a provided test. In this case, the test is `person.name.toLowerCase().includes(search.toLowerCase())`.

The code up to this point is as follows: 

```javascript
import React, { useState } from "react";

const App = (props) => {
  const people = [
    { name: "Alan Turing", number: "040-123456", id: 1 },
    { name: "Ada Lovelace", number: "39-44-5323523", id: 2 },
    { name: "Barbara Liskov", number: "12-43-234345", id: 3 },
    { name: "Mary Poppendieck", number: "39-23-6423122", id: 4 }
  ];

  const [persons, setPersons] = useState(props.people);
  const [search, setNewSearch] = useState("");

  const handleSearchChange = (e) => {
    setNewSearch(e.target.value);
  };

  const filtered = !search
    ? people
    : people.filter((person) =>
        person.name.toLowerCase().includes(search.toLowerCase())
      );

  return (
    <>
      <h2>Phone book</h2>
      Filter persons:{" "}
      <input type="text" value={search} onChange={handleSearchChange} />
      <h2>Numbers</h2>
    </>
  );
};

export default App;
```

The next and last step is to display the data on the webpage.

### Display data

To display the data on the webpage, you will map over the `filtered` array and display the appropriate list of people.

Write the following code after the "Numbers" heading.

```javascript
{filtered.map((person) => {
    return (
        <p key={person.id}>
            {person.name} - {person.number}
        </p>
    );
})}
```

The full code for the `App.js` is as follows:

```javascript
import React, { useState } from "react";

const App = (props) => {
  const people = [
    { name: "Alan Turing", number: "040-123456", id: 1 },
    { name: "Ada Lovelace", number: "39-44-5323523", id: 2 },
    { name: "Barbara Liskov", number: "12-43-234345", id: 3 },
    { name: "Mary Poppendieck", number: "39-23-6423122", id: 4 }
  ];

  const [persons, setPersons] = useState(props.people);
  const [search, setNewSearch] = useState("");

  const handleSearchChange = (e) => {
    setNewSearch(e.target.value);
  };

  const filtered = !search
    ? people
    : people.filter((person) =>
        person.name.toLowerCase().includes(search.toLowerCase())
      );

  return (
    <>
      <h2>Phone book</h2>
      Filter persons:{" "}
      <input type="text" value={search} onChange={handleSearchChange} />
      <h2>Numbers</h2>
      {filtered.map((person) => {
        return (
          <p key={person.id}>
            {person.name} - {person.number}
          </p>
        );
      })}
    </>
  );
};

export default App;
```

You are done! If you run the application, you should be able to search for particular people in the phonebook.

The application is live at this URL - [Phonebook searching and filtering](https://omq93.csb.app/).