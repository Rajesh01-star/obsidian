annotating a variable : setting the type of a variable 
eg -> let age : number
now age can only accept a number type value.

## configure the typescript compiler

```typescript
{
  "compilerOptions": {
    "target": "ES2016" 
    "module": "commonjs" 
    "rootDir": "./src"
    "sourceMap": true, /* this is for debugging */
    "removeComments": true,                           
    "noEmitOnError": true,                            
    "esModuleInterop": true 
    "forceConsistentCasingInFileNames": true 
    "strict": true 
    "skipLibCheck": true 
  }
}

```

## for debugging 
in the debugging panel 
	create a lauch.json file 
	
```ts
"program": "${workspaceFolder}/src/index.ts",
"preLaunchTask": "tsc: build - tsconfig.json",
"outFiles": [
"${workspaceFolder}/**/*.js"

]
```
this "preLaunchTask" line is need as it it so make sure to add it as it is with spaces.

so to launch a debugging session process follow the steps
1) for launching f5
2) for skipping over a line f10
3) for stopping the process shfit+f5
all the other shortcuts can be seen on the top bar above when debugging.

## builtin types
![builtin_types](public/images/buildinTypes.png)

you don't need to annotate all the variables typescript automatically detects the type when intialized
![autoAnnotate](public/images/autoAnnotate.png)
if  a variable is declared and not initialized then it's starting type will be __any__
-> so if the compiler has to implicitly add a any type to a variable it'll give an error so try to explicitly provide it 
![implicit](public/images/implicit.png)
## arrays
-> if you're going to use array and it should have only one type of data inside it ideally you can specify the type by
```typescript
let numbers : number[] = [1,2,3];
```
now if we try to add any other value that's not a number it'll give an error at compile time.
$$ GOOD GOOD $$
in vs code as we are using typescript and the editor knows the type of variable we're using it'll provide needed autocomplete out of the box.
## nice

## tuples
a tuple is a typed array with a pre-defined a length and types for each index.
tuples are great because they allow each element of an array to be a know type of value

```typescript
// define our tuple and initialize it
let user : [number,string] = [1,'atharv'];
```

so one gaps or fault in typescript tuples that even though the number of entries are defined as well as their types we can still push into the tuple which should not be allowed.

```typescript
let user : [number,string] = [1,'atharv'];
user.push('someone')
console.log(user);
```
so it should give error but it don't
![tuple_fault](public/images/tupleFault.png)

## enums

