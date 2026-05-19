
[Redux tutorial with sumit shara](https://www.youtube.com/watch?v=qhll3DXuLHI)
[Redux tutorial with code step by step](https://www.youtube.com/watch?v=66yHun4QLiI&list=PL8p2I9GklV46p1Gc33d8PXnpjZt3oDvhx)

# react project created

#### Create counter slice
three function uses
```js
import{createSlice} from '@reduxjs/toolkit'

export const counterSlice = createSlice({
    name:'counter',
    initialState: {count: 0},
    reducers:{
        increment:state=>{
            state.count = state.count+1
        },
        decrement:state=>{
            state.count = state.count+1
        },
        reset: state=>{
            state.count=0; 
        }
    }
})

export const {increment,decrement,reset} = counterSlice.actions;
export default counterSlice.reducer; 
```


#### Store create

```js

import {configureStore} from '@reduxjs/toolkit';
import counterReducer from './features/counter/counterSlice';

const store = configureStore({
    reducer:{
        counter: counterReducer,
    }
})

export default store;


```


#### Provider setup
into main.jsx

```js
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import {Provider} from 'react-redux'
import store from './app/store'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </StrictMode>,
)

```


#### how to use state value in react component

```js
import React from 'react'
import { useSelector } from 'react-redux'

const CounterView = () => {
    const count = useSelector((state) => state.counter.count)
    // const state = useSelector((state) => state)
    // console.log(state) // debug state into value

    // console.log(count)

    return (
        <div>
            <h4>Count: {count}</h4>
            <button>Increment</button>
        </div>
    )
}

export default CounterView

```

#### dispatch action 
```js
import React from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { increment } from './counterSlice';

const CounterView = () => {
    const count = useSelector((state) => state.counter.count)
    // const state = useSelector((state) => state)
    // console.log(state) // debug state into value

    // console.log(count)
    const dispatch = useDispatch();

    return (
        <div>
            <h4>Count: {count}</h4>
            <button onClick={()=>dispatch(increment())}>Increment</button>
        </div>
    )
}

export default CounterView

```

Three function uses:
```js
import React from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { decrement, increment, reset } from './counterSlice';

const CounterView = () => {
    const count = useSelector((state) => state.counter.count)
    // const state = useSelector((state) => state)
    // console.log(state) // debug state into value

    // console.log(count)
    const dispatch = useDispatch();

    return (
        <div>
            <h4>Count: {count}</h4>
            <button onClick={()=>dispatch(increment())}>Increment</button>
            <button onClick={()=> dispatch(decrement())}>decrement</button>
            <button onClick={()=>dispatch(reset())}>reset</button>
        </div>
    )
}

export default CounterView;

```





# redux toolkit where use

হ্যাঁ ✅ **React 18 install করে নেওয়াই তোমার জন্য সবচেয়ে ভালো (উপযোগী) হবে** — বিশেষ করে এখন যেহেতু তুমি Redux Toolkit শিখছো।

তোমার project এ এখন:

- React 19 ব্যবহার হচ্ছে
    
- আর `react-redux` এর সাথে compatibility issue হয়ে hook error দিচ্ছে
    

👉 React 18 এ নামালে এই problem চলে যাবে।

---

# 🎯 কেন React 18 ভালো হবে?

### ✅ 1️⃣ Stable ecosystem

Redux Toolkit + react-redux পুরোপুরি React 18 এ tested

### ✅ 2️⃣ Learning phase এ safest

তুমি যেহেতু Redux Toolkit শিখছো, version issue নিয়ে সময় নষ্ট করার দরকার নেই

### ✅ 3️⃣ Industry standard

এখনও অনেক production app React 18 ব্যবহার করছে

---

# 🔧 কীভাবে install করবে (Correct Way)

Project folder এ গিয়ে চালাও:

```bash
npm install react@18.2.0 react-dom@18.2.0
npm install -D @types/react@18 @types/react-dom@18
```

তারপর clean install:

```bash
rm -rf node_modules
rm package-lock.json
npm install
npm run dev
```

---

# 📌 Final Advice

👉 এখন React 18 use করো  
👉 Redux Toolkit practice করো  
👉 পরে React 19 fully stable হলে upgrade করবে

---



# Read books crud project

https://www.youtube.com/watch?v=qwNuYbxVIYk
1. project setup
2. store add 
3. feature add
4. 
reducer setup