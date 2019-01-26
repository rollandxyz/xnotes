https://stackblitz.com/

```js
mapExample() {
    const myMap = new Map();

    const keyString = 'a string',
    keyObj = {},
    keyFunc = function() {};
    // setting the values
    myMap.set(keyString, 'value associated with "a string"');
    myMap.set(keyObj, 'value associated with keyObj');
    myMap.set(keyFunc, 'value associated with keyFunc');

    console.log(myMap.size); // 3

    // getting the values
    myMap.get(keyString);    // "value associated with 'a string'"
    myMap.get(keyObj);       // "value associated with keyObj"
    myMap.get(keyFunc);      // "value associated with keyFunc"

    myMap.get('a string');   // "value associated with 'a string'"
                            // because keyString === 'a string'
    myMap.get({});           // undefined, because keyObj !== {}
    myMap.get(function() {}); // undefined, because keyFunc !== function () {}

    const pMap = new Map();
    pMap.set(0, 'zero');
    pMap.set(1, 'one');
    pMap.forEach(value => {

    });

    pMap.forEach((value: boolean, key: string) => {
      console.log(key, value);
    });
    for (const [key, value] of Object.entries(pMap)) {
      console.log(key, value);
    }

    for (const entry of Array.from(pMap.entries())) {
      const key = entry[0];
      const value = entry[1];
    }

    // Iterate over the keys
    Array.from(pMap.keys()).forEach(key => console.log(key));

    // Iterate over the values
    Array.from(myMap.values()).forEach(value => console.log(value));

    // Iterate over the entries
    Array.from(myMap.entries()).forEach(entry => console.log('Key: ' + entry[0] + ' Value: ' + entry[1]));

    Object.keys(myMap).map( key => {
      console.log('key: ' + key);
      console.log('value: ' + myMap[key]);
    });
    /*
    for (const [key, value] of pMap) {
      console.log(key + ' = ' + value);
    }

    for (const key of pMap.keys()) {
      console.log(key);
    }

    for (const value of pMap.values()) {
      console.log(value);
    }

    for (const [key, value] of pMap.entries()) {
      console.log(key + ' = ' + value);
    }
    */
  }
  ```
