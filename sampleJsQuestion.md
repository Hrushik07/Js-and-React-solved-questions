## Js and React solved techinical questions

q1.solve this
<br>
[0,1,0,8,8,8,0]<br>
output:- [1,8,8,8,0,0,0]

<details><summary>Answer</summary>

```js
let arr = [0,1,0,8,8,8,0]

for(let i = 0 ; i < arr.length ; i++){
 if(arr[i]==0){
   arr.splice(i,1);
   arr.push(0)
 }
}

console.log(arr)
```
</details>

---
q2.sort an array without using inbuilt methods if you are using for loop use only one for loop.
<br>

<details><summary>Answer</summary>

```js
let arr = [5, 2, 9, 1, 5, 6];

for (let i = 0; i < arr.length - 1; ) {
  let j = i + 1;
  if (arr[i] > arr[j]) {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    i = 0; 
  } else {
    i++; 
  }
}

console.log(arr);
```
</details>

---

q3. You have a credit card number "1234567812345678" and need to display it as "************5678" ?
<br>

<details><summary>Answer</summary>

```js
let str="1234567812345678"
let res=""
for (let i=0;i<str.length;i++)
{
    if(i<str.length-4)
    {
        res=res+"*"
    }
    else{
        res=res+str[i]
    }
}
console.log(res);

```
</details>

---

Q4. Create an application with two buttons i.e (Add new and Clear All)
<br>
(i) Whenever we click on the Add new button, a row should open which contains day, start time and end time, if we click the Add new button multiple times, then corresponding to that multiple rows to come.
<br>
(ii) And if we click on clearAll button, all the rows should be cleared.

<details><summary>Answer</summary>

```js
import React, { useState } from "react";

const TimeScheduler = () => {
  const [rows, setRows] = useState([]);

  const addRow = () => {
    setRows([...rows, { day: "", startTime: "", endTime: "" }]);
  };

  const clearAll = () => {
    setRows([]);
  };

  const handleChange = (index, field, value) => {
    const updatedRows = [...rows];
    updatedRows[index][field] = value;
    setRows(updatedRows);
  };

  return (
    <div>
      <h2>Time Scheduler</h2>
      <button onClick={addRow}>Add New</button>
      <button onClick={clearAll}>Clear All</button>
      <table border="1" style={{ marginTop: "10px", width: "100%" }}>
        <thead>
          <tr>
            <th>Day</th>
            <th>Start Time</th>
            <th>End Time</th>
          </tr>
        </thead>
        <tbody>
          {rows.map((row, index) => (
            <tr key={index}>
              <td>
                <input
                  type="text"
                  value={row.day}
                  onChange={(e) => handleChange(index, "day", e.target.value)}
                />
              </td>
              <td>
                <input
                  type="time"
                  value={row.startTime}
                  onChange={(e) =>
                    handleChange(index, "startTime", e.target.value)
                  }
                />
              </td>
              <td>
                <input
                  type="time"
                  value={row.endTime}
                  onChange={(e) =>
                    handleChange(index, "endTime", e.target.value)
                  }
                />
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default TimeScheduler;

```

</details>

---

Q5. Write a program to find the second largest number in an array

<details><summary>Answer</summary>

```js
import React, { useState } from "react";

const SecondLargestNumber = () => {
  const [numbers, setNumbers] = useState([10, 20, 5, 30, 30, 25, 15]);
  const [secondLargest, setSecondLargest] = useState(null);

  const findSecondLargest = () => {
    const uniqueNumbers = [...new Set(numbers)]; 
    if (uniqueNumbers.length < 2) {
      setSecondLargest("Not enough elements");
      return;
    }
    uniqueNumbers.sort((a, b) => b - a); 
    setSecondLargest(uniqueNumbers[1]); 
  };

  return (
    <div style={{ padding: "20px" }}>
      <h3>Array: {JSON.stringify(numbers)}</h3>
      <button onClick={findSecondLargest}>Find Second Largest</button>
      {secondLargest !== null && <h4>Second Largest: {secondLargest}</h4>}
    </div>
  );
};

export default SecondLargestNumber;
```

</details>

---
q6. Rotate the elements in an array with respect to its index.(with inbuild method)
<br>
Let arr=[1,2,3,4,5,6]
index=2
<br>
Output=[3,4,5,6,1,2]

<details><summary>Answer</summary>

```js
let arr = [1, 2, 3, 4, 5, 6];
let index = 2;

let rotatedArr = arr.slice(index).concat(arr.slice(0, index));

console.log(rotatedArr);
```
</details>

---
Q7. Rotate the elements in an array with respect to its index.(without inbuild method)
<br>
Let arr=[1,2,3,4,5,6]
index=2
<br>
Output=[3,4,5,6,1,2]

<details><summary>Answer</summary>

```js
// with only one for loop
let arr = [1, 2, 3, 4, 5, 6];
let index = 2;
let rotatedArr = [];

for (let i = 0; i < arr.length; i++) {
  let newIndex = (index + i) % arr.length;
  rotatedArr.push(arr[newIndex]);
}

console.log(rotatedArr);

//we can do this using two for loops

let arr = [1, 2, 3, 4, 5, 6];
let index = 2;
let rotatedArr = [];

for (let i = index; i < arr.length; i++) {
  rotatedArr.push(arr[i]);
}

for (let i = 0; i < index; i++) {
  rotatedArr.push(arr[i]);
}

console.log(rotatedArr);

```
</details>

---

Q8. We have a button called add circle. Whenever we click on that circle, it should create circle and also the count should increase. Whenever you click on the circle, the circle background color should change to Grey color and also the count should increase. If we once again click on that circle background, the color should change into white and there should be a decrease in the count.

<details><summary>Answer</summary>

```js
import React, { useState } from "react";

const CircleApp = () => {
  const [circles, setCircles] = useState([]); 
  const [count, setCount] = useState(0); 

  const addCircle = () => {
    setCircles([...circles, { id: circles.length, isGray: false }]);
    setCount(count + 1);
  };

  const toggleCircleColor = (id) => {
    setCircles((prevCircles) =>
      prevCircles.map((circle) =>
        circle.id === id ? { ...circle, isGray: !circle.isGray } : circle
      )
    );

    setCount((prevCount) =>
      circles.find((circle) => circle.id === id)?.isGray
        ? prevCount - 1
        : prevCount + 1
    );
  };

  return (
    <div style={{ padding: "20px", textAlign: "center" }}>
      <h3>Count: {count}</h3>
      <button
        onClick={addCircle}
        style={{ padding: "10px", marginBottom: "20px" }}
      >
        Add Circle
      </button>
      <div
        style={{
          display: "flex",
          gap: "10px",
          flexWrap: "wrap",
          justifyContent: "center",
        }}
      >
        {circles.map((circle) => (
          <div
            key={circle.id}
            onClick={() => toggleCircleColor(circle.id)}
            style={{
              width: "50px",
              height: "50px",
              borderRadius: "50%",
              backgroundColor: circle.isGray ? "gray" : "white",
              border: "2px solid black",
              cursor: "pointer",
            }}
          ></div>
        ))}
      </div>
    </div>
  );
};

export default CircleApp;
```


</details>

---

Q9. const arr = ['hello', 'sky', 'cloud']; <br>
Without using inbuilt methods and if using loops, use only one loop and find the number of vowels in each element of the given array.  
<br>
Output array should be ['2', '0', '2']

<details><summary>Answer</summary>

```js
const arr = ["hello","sky","cloud",]
let str = arr+","
const vowels="aeiou"
console.log(typeof vowels)
let countarr= []
let count = 0 ;

for(let i = 0 ; i < str.length ;i++){
   
    if(vowels.includes(str[i])) {
        count ++;
    }
    
    if(str[i]===','){
      countarr.push(count)
      count = 0;
    }
}

console.log(countarr)
```

</details>

---







