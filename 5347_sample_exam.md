# **Exercise One**

a) Referring to the tutorial exercise in week 3, can you tell the difference between `p#reviews_p` and `#reviews p`? 



`p#reviews_p` 和 `#reviews p` 是两种不同的 CSS 选择器，用于选择页面上的元素，它们的区别在于所选择的元素类型和范围

`p#reviews_p` 选择器：

- 选择带有特定ID的段落元素（`<p>`）。
- `p#reviews_p` 选择器表示选择一个段落元素（`<p>`），该段落元素的ID为`reviews_p`。

```html
<p id="reviews_p">Hello World!</p>
```

```javascript
let ele = document.querySelector('p#reviews_p')
```

`#reviews p` 选择器：

- 选择某个ID的元素内部的所有段落元素（`<p>`）。
- `#reviews p` 选择器表示选择ID为`reviews`的元素内部的所有段落元素（`<p>`）。

```html
<div id="reviews">
    <p>
        Hello World!
    </p>
    <p>
        Hello Html
    </p>
</div>

<script>
	let ele = document.querySelectorAll('#reviews p')
</script>
```



b) Can you name more CSS selectors, what about their priorities, and in which situation they will be overwritten?

1. **元素选择器**（Type Selector）
   - 选择所有指定类型的元素，例如 `p` 选择所有段落元素 `<p>`。
   - 示例：`p { color: red; }`
2. **类选择器**（Class Selector）
   - 选择所有具有指定类名的元素，使用 `.` 表示。
   - 示例：`.class-name { color: blue; }`
3. **ID 选择器**（ID Selector）
   - 选择具有指定ID的唯一元素，使用 `#` 表示。
   - 示例：`#id-name { color: green; }`
4. **属性选择器**（Attribute Selector）
   - 选择具有指定属性的元素。
   - 示例：`[type="text"] { color: gray; }`
5. **伪类选择器**（Pseudo-class Selector）
   - 选择特定状态的元素，例如鼠标悬停时的元素。
   - 示例：`a:hover { color: orange; }`
6. **伪元素选择器**（Pseudo-element Selector）
   - 选择元素的特定部分，例如第一个字母或内容前后的内容。
   - 示例：`p::first-letter { font-size: 2em; }`
7. **组合选择器**（Combinator Selector）
   - 选择特定关系的元素，例如子元素、相邻兄弟元素等。
   - 示例：`div > p { color: purple; }` 选择所有作为 `div` 子元素的 `p`。
8. **后代选择器**（Descendant Selector）
   - 选择某个元素内部的所有指定后代元素。
   - 示例：`div p { color: brown; }` 选择所有 `div` 内的 `p` 元素。

**CSS 选择器优先级**

CSS 选择器的优先级由以下规则确定：

1. **内联样式**（Inline Style）：优先级最高。
   - 例如：`<p style="color: red;">`，优先级值：`1000`
2. **ID 选择器**：次高优先级。
   - 例如：`#id-name`，优先级值：`100`
3. **类选择器、属性选择器、伪类选择器**：中等优先级。
   - 例如：`.class-name`，优先级值：`10`
4. **元素选择器、伪元素选择器**：优先级最低。
   - 例如：`p`，优先级值：`1`

如果有多个选择器应用于同一个元素，且设置了相同的属性，优先级较高的选择器样式会覆盖优先级较低的选择器样式。如果优先级相同，则最后声明的样式会覆盖之前的样式。

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p { color: black; }              /* 优先级 1 */
    .class-name { color: blue; }     /* 优先级 10 */
    #id-name { color: green; }       /* 优先级 100 */
    p#id-name { color: red; }        /* 优先级 101 */
  </style>
</head>
<body>
  <p id="id-name" class="class-name">Hello World!</p>
</body>
</html>
```



# **Exercise Two**

In an Express.js application, explain how you would define a MongoDB schema using Mongoose for a shopping item (for example, cloth) collection that includes fields for title, category, image, price, stock, and sizes. Provide a sample schema definition.

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const clothSchema = new Schema({
  title: {
    type: String,
    required: true,
    trim: true,
  },
  category: {
    type: String,
    required: true,
    trim: true,
  },
  image: {
    type: String,
    required: true,
    trim: true,
  },
  price: {
    type: Number,
    required: true,
    min: 0,
  },
  stock: {
    type: Number,
    required: true,
    min: 0,
  },
  sizes: {
    type: [String],
    required: true,
  },
}, {
  timestamps: true,
});

const Cloth = mongoose.model('Cloth', clothSchema)

module.exports = Cloth
```



# **Exercise Three**

Answer the following questions based on the script below.

```javascript
var express = require('express')
var app = express()
var seq = 1

// 中间件 middleware function
app.use(function(req, res, next){
    console.log('Request ' + seq + ': ' + req.url) // 打印 seq 和 请求的 url
    seq++ // 每请求一次就会增加1次
    next() // 将控制权传递给栈中的下一个中间件函数 
})

// 路由 监听get请求并且根路径为 '/'
app.get('/', function(req, res){
    res.send('Hello World!') // 访问根路径时，会响应'Hello World!'
})

// 路由 监听'/greeting'
app.get('/greeting', function(req, res){
    var name = "World" // 初始化一个变量并赋值 World
    if (req.query.name) // 如果请求中name不为空
        	name = req.query.name // 将请求中的name赋值给name
    res.send("Hello " + name) // 响应Hello 和 name
})

// 启动Express服务器，端口为3000
app.listen(3000, function () {
    console.log('greeting app listening on port 3000!') //输出
})
```

a) Explain what the code from **line 5 to line 9** and from **line 15 to line 20** is supposed to do. Make sure to use appropriate technical terms and concepts in your answer.

5 - 9：

- This middleware function logs each incoming request to the console.
- It logs the request number (`seq`) and the request URL (`req.url`).
- The `seq` variable is incremented after each request.
- The `next()` function is called to pass control to the next middleware function in the stack.

15 - 20：

- This defines a route that listens for GET requests on the `/greeting` path.
- It initializes `name` to "World".
- If the request includes a query parameter `name`, it updates the `name` variable with the value of `req.query.name`.
- It responds with "Hello " followed by the value of `name`.



b) Suppose the URL of the first request sent to the application is **localhost:3000/greeting.** What output will the application produce when it receives the provided request?

1. consoles: 'Request 1: /greeting' (控制台输出)
2. response: Hello World (浏览器返回响应结果)



c) Suppose the URL of the second request sent to the application is **http://localhost:3000/greeting?title=node.js.** What output will the application produce when it receives the provided request?

1. consoles: 'Request 2: /greeting?title=node.js' (控制台输出)
2. response: Hello World (浏览器返回响应结果)



d) Suppose the URL of the third request sent to the application is **http://localhost:3000/.** What output will the application produce when it receives the provided request?

1. consoles: 'Request 3: /' (控制台输出)
2. response: Hello World! (浏览器返回响应结果)



# **Exercise Four**

You have been tasked with developing a new feature for a local library's website. One feature is a form that allows library members to request books by inputting the book's ISBN (e.g. **978-3-16-148410-0**). Unfortunately, some members have been entering incorrect ISBNs, causing delays and confusion in the book request process. To address this issue, you decide to implement a validation feature for the form.

Write a JavaScript function that validates the ISBN input when the form is submitted. The function should check if the ISBN is in the correct format (e.g., a 13-digit number). If the ISBN is not in the correct format, the function should display an alert message to the user indicating that the validation fails.

Sample HTML file:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Library Book Request</title>
    <script src="script.js"></script>
</head>
<body>
    <form id="isbnForm">
        <label for="isbn">Enter ISBN:</label>
        <input type="text" id="isbn" name="isbn" required>
        <button type="submit">Request Book</button>
    </form>
</body>
</html>
```

```javascript
document.addEventListener('DOMContentLoaded', function() {
    // 获取表单元素
    let form = document.getElementById('isbnForm')
    
    // 监听表单提交事件
    form.addEventListener('submit', function(event) {
        // 获取输入的ISBN
        let isbnInput = document.getElementById('isbn').value
        
        // 调用验证函数
        if (isValidISBN(isbnInput)) {
            // 如果验证失败，阻止表单提交并显示错误消息
            event.preventDefault()
            alert('Invalid Input!')
        }
    })
});

function isValidISBN(isbn) {
    // 移除所有的连字符
    let cleanedISBN = isbn.split('-').join('');
    
    // 检查是否为13位数字
    if (cleanedISBN.length !== 13){
        return false
    }
    
    for (let i = 0; i < cleanedISBN.length; i++){
        if (cleanedISBN[i] < '0' || cleanedISBN[i] > '9'){
            return false
        }
    }
    
    return ture;
}
```



# **Exercise Five**

You are a web developer for a popular e-commerce site. The main page will display a list of items with images, titles, prices, etc.

a) Identify and describe some elements or factors in an HTML document that could potentially affect page load time and render performance.

1. 外部资源加载：
   - JavaScript：外部JavaScript文件在加载和解析时会阻塞HTML的解析（External JavaScript files block HTML parsing when loaded and parsed.）
   - CSS：外部CSS文件需要在渲染页面之前加载解析，因为它们影响页面的布局和样式（External CSS files need to be loaded and parsed before rendering the page because they affect the layout and style of the page.）
2. 静态资源：
   - 大量的图片和视频文件需要时间加载，特别是如果它们未被优化或尺寸过大 （Large image and video files take time to load, especially if they are unoptimized or oversized.）
3. 同步：
   - 如果脚本在 `js` 部分以同步方式加载（例如，没有使用 `async` 或 `defer` 属性），会阻塞页面的渲染（If the javascript is loaded synchronously in the head section (for example, without using the async or defer attributes), it will block the rendering of the page.）
4. 复杂的DOM结构：
   - 过于复杂和嵌套过深的 DOM 结构会增加浏览器解析和渲染的时间（Overly complex and deeply nested DOM structures can increase browser parsing and rendering time.）

b) Discuss the concept of the critical rendering path and how it relates to page load time.

Critical rendering path (CRP) are the steps the browser takes from receiving the HTML to fully rendering the page.

1. HTML
   - Browser parses HTML, generates DOM tree
2. CSS
   - Browser parses CSS, generates CSSOM tree
3. DOM and CSSOM
   - Combining DOM and CSSOM to generate a rendering tree
4. Layout
   - Calculate the position and size of each element based on the rendering tree
5. Rendering
   - Drawing each element to the screen



c) Identify a potential render-blocking resource and suggest a strategy to minimize its impact on page load time.

1. JavaScript
   - Use async or defer attributes to load scripts asynchronously to avoid blocking HTML parsing.
   - Place non-critical JavaScript files at the bottom of the page.
   - Merge and minimize JavaScript files.
2. CSS
   - Reduce HTTP requests by embedding critical CSS directly into HTML (inline CSS).
   - Use media queries to delay loading non-critical CSS (e.g., stylesheets for printing).
   - Merge and minimize CSS files.
3. Static resources
   - Optimize image size and format
4. DOM
   - Simplify the DOM structure to minimize levels of nesting.
   - Use efficient CSS selectors to avoid impacting rendering performance.
5. Synchronization Script
   - Try to avoid using synchronized scripts in the head section. Use the async or defer attributes to load scripts.



# **Exercise Six**

Referring back to your assignment 2, please answer the following two questions:

a) Explain in detail the benefits of using the Model-View-Controller (MVC) architecture in your A2 web application development.

Using the MVC architecture significantly improves the maintainability and testability of web applications. By separating the model, view, and controller, developers are able to develop and test each component independently. This separation also facilitates code reuse and parallel development, increasing development efficiency. MVC makes applications more flexible and extensible, making it easier to change user interfaces or modify business logic, while simplifying the management of complex applications. （可维护性和可测试性，通过分离模型、视图和控制器，开发人员能够独立开发和测试各个组件。这种分离还促进了代码重用和并行开发，提高了开发效率。MVC 使应用程序更加灵活和可扩展，可以更容易地更换用户界面或修改业务逻辑，同时简化复杂应用程序的管理）



b) Describe in detail the concept and usage of each component in MVC architecture (e.g. models, views, controller, route, middleware) in your A2 web application development.

1. Model: handles data and business logic for applications, interacts with databases, performs data manipulation and validation.
   - usage: 
     - Data Management: Models define data structures and methods for create, read, update, and delete (CRUD) operations.
     - Operational Logic: The model contains operational logic and rules
2. View: Responsible for presenting the data to the user, i.e. the user interface part, formatting and displaying the data of the model.
   - usage:
     - User Interface Rendering: A view formats the model's data into a form that the user can understand and interact with. It can be an HTML page, template, or other user interface component.
     - Update Interface: As model data changes, the view updates the interface to reflect those changes.
3. Controller: Receives user input, calls the model to process the data, and selects the appropriate view to display the results, coordinating the interaction between the model and the view.
   - usage:
     - Processing requests: The controller processes the user's requests (e.g., via URL paths and query parameters), calls the appropriate model methods, and decides which view to use to render the response.
     - Updating the model and view: the controller updates the model's data based on the user's actions and notifies the view to update its display.



c) Referring to the starter code provided in weeks 5 and 6 tutorials, how will you refactor the non-MVC structure to the MVC one?
