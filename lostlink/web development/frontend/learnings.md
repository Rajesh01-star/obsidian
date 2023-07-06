in forms if you have to add validation on input so that it'll not submit unfilled 
then 
```javascript
<form onSubmit={(e)=>e.preventDefault()}>
	<input name='fname' type="text" required />
	...
	<button type='submit'>SUBMIT</button>
</form>
```
