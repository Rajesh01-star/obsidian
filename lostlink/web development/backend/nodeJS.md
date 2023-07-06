to use import / export in nodeJS = pacakage.json add 

```js
  "type": "module",
```
-> if you're using ES6 in node then whenever you're exporting a custom function from a file the file should be names  __fileName.mjs__ .

## So I found out a new WAY
well at least for my-self it was new
so there is back-end which does -> routing,storing,validting
front-end -> show business 

my-way back-end two files
1) one for getting data from the hosting platforms
2) one for routing different pages when request is made
 they communicate with each other to make full back-end.



## EJS
-> in a node project first install everything including ==ejs== 
-> make a ==views== folder in "root" directory

```js
const app = express();
app.set('view engine','ejs');
app.get("/",(req,res)=>{
res.render('base',{title:"rajesh"})

})
```

### if else statements in ejs

```js
<% if(title === "rajesh" || title == "atharv"){ %>
	<h1>you're the owner</h1>
<% } else { %>
	<h1>you're not the owner </h1>
}
```

so ejs is a combination of html with some javascript power
when writing normal html it's all good
access variable within html = <%=variable_name%>
control statement example is above .

in-case you need to pass variables from one ejs file to another then

```ejs
<%- include("partials/header", { titleSite: titleSite }) -%>
```

->say you have a variable which value is some html content and you need to render that html content as html and not as plain text then 

```ejs
<%- individualBlog.htmlContent %>
```
**<%-*** is important to see here and not **<%=** [[minimal_blog]]

