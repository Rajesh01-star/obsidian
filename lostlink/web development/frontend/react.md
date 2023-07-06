you can only use hooks inside a functional component.
hooks execute in a sequential order that they are defined in ...
can not define / use hooks inside a condition statement
## useState

- if there's any complex calculation to set the state for the first time (default state) then make sure it's an expression so that it'll be run only one time.
```javascript
function demo(){
console.log("run demo function");
return 4;
}

function App() {
const [count,setCount] = useState(demo);
..
}
```

when the state changes it re-renders the whole component that is returning in the top level
so if we "set" any value using useState without any conditions then it's going to re-render the component and it's going to be in a infinite loop
```javascript
import React,{useState} from "react";

export default function App(){
const [newItem,setNewItem] = useState("");
setNewItem("Atharv");
return(
	<form>
		<input type="text" value={newItem} />
	</form>
)
}
```
--->here the "setNewItem" is changing right in the top level code without any condition and will cause the component to go into an infinite loop.

## useEffect

it basically works as a side effect to anything in the website that it is attached to .
```javascript
useEffect(()=>{
console.log("rendered");
});
```
--> it'll run every time the application renders if no dependencies are there.

- if you only want to run the hook only if a certain value changes then you can add that to the dependency array
- so if you're using some kind of eventListener or subscribing to any api in the useEffect and afterwards the component may remain unused, you need to clean up that side effect by returning a clean up function 
```javascript
useEffect(()=>{
	window.addEventListener("resize",resizeHandler);
return ()=>{
	window.removeEventListener("resize",resizeHandler);
}
})
```


## useMemo
- so if anything changes inside a component the whole component re-renders right
- so if there's a slow part of the component that doesn't actually need to re-run everytime any other part of the component changes but it re-run anyway that slows down our site.
- to avoid that useMemo is used.
- it caches the enveloped code into memory so that if anything other than the dependency array changes it doesn't re-run.

```javascript
const doubleNumber = useMemo(()=>{
	return slowFunction(number);
},[number])
```
here slowFunction is cached into the memory and only re-runs if the **number** changes.

- in javascript even though some function / variables are explicitly made equal, they actually reference different objects in the stack.

```javascript
const themeStyle = {
backgroundColor:dark ? 'black' : 'white',
color:dark? 'white' : 'black',
width:'10rem',
}
```
when the component re-renders the themeStyle object again gets created but this time at different memory location that causes it to re-render also.
we only want to re-render if they are changed or they are not so bigger part of the component.
so we can use "useMemo" hook here to save us some performance time

```javascript
const themeStyle = useMemo(()=>{
	return {
		backgroundColor:dark ? 'black' : 'white',
		color:dark? 'white' : 'black',
		width:'10rem',
	}
},[dark])
```
here only the **dark** variable is to change so that's in the dependency array.


## useRef
useRef is almost as same as useState, but
- useRef persists between renders unlike state
- it doesn't cause the component to re-render.

```javascript
const renderCount = useRef(1);

return <div>I rendered {renderCount.current} times.</div>
```

here unlike **state** , useRef returns only one **object** and that only has one property **current** that stays between renders.

example set an input to focus on click of a button

```javascript
const inputRef = useRef();
function focus(){
	inputRef.current.focus();
}

return(
	<input ref={inputRef} type="text" />
	<button onClick={focus}>Focus</button>
)
```

- useRef can also be used to store the previous value of the state.

```javascript
const [name,setName] = useState('');
const prevName = useRef();

useEffect(()=>{
	prevName.currenct = name;
},[name])

return(
	<input type="text" value={name} onChange((e)=> setName(e.target.value)) />
	<div>My name is {name}, and it used to be {prevName}</div>
)
```



## useReducer
- also allows user to manage state and re-render a component whenever the state changes.
reducer takes 2 things and returns an array of 2 objects 
```javascript
const [state,dispatch] = useReducer(reducer,{count:0})
```
**reducer** is a function here that you can call by **dispatch** 
```javascript
function reducer(state,action){
    switch (action.type){
        case 'increment':
            return {count : state.count + 1}
        case 'decrement':
            return {count : state.count - 1}
        default:
            return state;
    }
}

export default function Reducer(){
    const [state,dispatch] = useReducer(reducer,{count:0})

    function increment(){
        dispatch({type:"increment"});
    }
    function decrement(){
        dispatch({type:"decrement"});
    }
    ...
    }
```




## controlled components
in react html form components can either be self valued or it's value can be controlled by the react hooks so that there will be only one source of truth
```javascript
export default function App(){
	const [data,setData] = useState();
	const handleInput = (e)=>{
		setData = e.target.value;
	}
	return(
		<form action="/blogs" method="POST">
			<input onChange={handleInput} value={data} />
			<button type="submit">submit</button>
		</form>
	)
}
```
this way you can now pass the value to other UI elements too, or reset it from other event handlers.

## textarea tag

In HTML textarea defines it's text as it's children
but in react textarea uses a value attribute instead so it's similar to single line input tag
