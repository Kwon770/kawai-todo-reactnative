# Kawai To Do

Kawai To Do App made with React Native

## The things what i learn

### react-native-uuid

Use **'react-native-uuid'** from Reactnative, instead of 'uuid'

'uuid' isn't recognized (tested on Expo)

```js
$ yarn add react-native-uuid
$ npm install react-native-uuid

import uuid from "react-native-uuid";

const ID = uuid.v1();
```

### prevState Argument

**prevState** is the argument passed to `setState` callback function

It it the value of state before `setState` was triggered by React

```js
_deleteToDo = id => {
  this.setState(prevState => {
    delete prevState.toDos[id];
    return { ...prevState };
  });
};
```

### Object name with variable or string

- \[variable]: {}
- "string": {}

```js
const object = {
  [ID]: {
    id: ID,
    isBool: false
  }
};

const object = {
  string: {
    id: "string1",
    isBool: false
  }
};
```

### Variable get value from Object by reference type

```js
obj = { a: "b" };
console.log(obj); // {"a": "b"}

const temp = obj;
delete temp["a"];
console.log(obj); // {}
```

### Auto overwrite from object

if there is overlapping code, the code below is overlapping

```js
_uncompleteToDo = id => {
  this.setState(prevState => {
    const newState = {
      ...prevState,

      // Overlapping to toDos of prevState
      toDos: {
        ...prevState.toDos,

        // Overlapping to [id] of prevState.toDos
        [id]: {
          ...prevState.toDos[id],

          // Overlapping to isComplete of prevState.toDos[id].isCompleted
          isCompleted: false
        }
      }
    };
    return { ...newState };
  });
};
```
