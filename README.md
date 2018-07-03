# promise_all_reflect
Promise.all with reflect for waiting all promises completed

### Reflect

```
const reflect = p => p.then(
  v => ({ v, status: "fulfilled" }),
  e => ({ e, status: "rejected" })
);
```

### sample.js

```
// Create array of promises for testing with random setTimeout
var myArr = []
for(let i=0;i<10;i++) {
  myArr.push(new Promise((resolve, reject) => {
    let random_max = 1000;
    let sec = Math.floor((Math.random()*random_max)+1)
    console.log("#"+i+" setTimeout="+sec);
    setTimeout(() => {
      console.log("#"+i+" done.");
      if(sec >= random_max/2) {
        resolve("Resolved #"+i)
      } else {
        reject("Rejected #"+i)
      }
    }, sec)
  }))
}

// Reflect
const reflect = p => p.then(
  v => (
    { v, status: "fulfilled" }
  ),
  e => (
    { e, status: "rejected" }
  )
);

// Promise.all
Promise.all(myArr.map(reflect)).then((results) => {
  console.log(results);
})
```
