# Kawai To Do

Kawai To Do App made with React Native

## The things what i learn

### 1. react-native-uuid

Use **'react-native-uuid'** from Reactnative, instead of 'uuid'

'uuid' isn't recognized (tested on Expo)

```js
$ yarn add react-native-uuid
$ npm install react-native-uuid

import uuid from "react-native-uuid";

const ID = uuid.v1();
```

### 2. prevState Argument

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

### 3. bject name with variable or string

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

### 4. Variable get value from Object by reference type

```js
obj = { a: "b" };
console.log(obj); // {"a": "b"}

const temp = obj;
delete temp["a"];
console.log(obj); // {}
```

### 5. Auto overwrite from object

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

### 6. Ui propagation(전파) problem

when the ui occur event, this event propagate event to related event

_From this project, button [\<TouchableOpacity>] propagte event to scrollView_

To prevent this, ```event.stopPropagation()``` must be written

```js
render() {
  ~~

  <TouchableOpacity onPressOut={event => {
                event.stopPropagation();
                deleteToDo(id);
              }}>
              
              ~~~

  </TouchableOpacity>

  ~~
}
```

### 7. The error what can be occured during loading save-data

When the app operate first, the problem can be occured during load proccess

Because there is no key (data key) on first operation, ```AsyncStorage.getItem("key")```  return null or undefinded

so you must prevent this exceoption

```js
_loadToDos = async () => {
    try {
      const toDos = await AsyncStorage.getItem("toDos"); // Error is occured on first operation
      const parsedToDos = JSON.parse(toDos);
      this.setState({
        loadedToDos: true,
        toDos: parsedToDos || {} // To prevent error, when loading data is null, return {}
      });
    } catch (err) {
      console.log(err);
    }
  };
```

### 8. Setting app.json to publish by expo

android package must be written in app.json

```json
"android": {
  "package": "com.yourcompany.yourname"
},

"ios": {
  "supportsTablet": true
}
```