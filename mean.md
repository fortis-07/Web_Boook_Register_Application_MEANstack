# MEAN Stack

The MEAN stack is a full-stack JavaScript ecosystem for developing web applications, leveraging a unified language across the entire development stack. It comprises four core technologies: MongoDB, Express.js, Angular, and Node.js. Each component serves a specific function in the application architecture, synergizing to create a robust and efficient web development environment.

## Stack Components

### MongoDB
MongoDB is a schema-less, document-oriented NoSQL database that utilizes BSON (Binary JSON) for data storage. Its flexible data model facilitates dynamic schema evolution and supports horizontal scaling through sharding. MongoDB's query language and indexing capabilities enable efficient data retrieval and manipulation, making it ideal for handling unstructured or semi-structured data in web applications.

### Express.js
Express.js is a minimalist web application framework for Node.js, following the middleware pattern. It provides a robust set of features for building RESTful APIs and web applications. Express.js simplifies HTTP request handling, routing, and middleware integration. Its modular architecture allows for easy extension and integration with other Node.js libraries, enhancing server-side functionality.

### Angular
Angular is a TypeScript-based front-end framework that implements the Model-View-ViewModel (MVVM) architectural pattern. It utilizes a component-based architecture, facilitating the development of Single Page Applications (SPAs). Angular's key features include:
- Dependency Injection (DI) for modular and testable code
- RxJS for reactive programming and asynchronous operations
- Angular CLI for scaffolding and build optimization
- TypeScript support for enhanced type checking and OOP paradigms

### Node.js
Node.js is an event-driven, non-blocking I/O runtime built on the V8 JavaScript engine. It enables server-side JavaScript execution, leveraging an event loop for handling asynchronous operations efficiently. Node.js's package ecosystem, npm, provides access to a vast library of reusable modules. Its asynchronous nature and event-driven architecture make it highly scalable for concurrent connections and real-time applications.

## MEAN Stack Advantages

1. Isomorphic JavaScript: Unified language usage across client and server, reducing context switching and enabling code reuse.

2. JSON-centric data flow: Seamless data serialization and deserialization between all stack layers.

3. Scalability: Horizontal scaling capabilities of MongoDB and Node.js's non-blocking architecture enable handling high concurrent loads.

4. Real-time capabilities: WebSocket support in Node.js and Angular's change detection mechanism facilitate real-time application development.

5. Modular architecture: Component-based design in Angular and middleware approach in Express.js promote code reusability and maintainability.

6. Rich ecosystem: Extensive npm registry and active community support accelerate development through third-party modules and resources.

The MEAN stack's cohesive JavaScript-based architecture, coupled with its scalability and performance characteristics, makes it a compelling choice for modern web application development, particularly for projects requiring real-time features and flexible data models.

In order to complete this project, you will need an AWS account and a virtual server with Ubuntu Server OS.

### Pre-requisite

- Create a new EC2 instance of the t2.micro family with Ubuntu Server 24.04 LTS (HVM) image and SSH into the Instance

![WhatsApp Image 2024-09-25 at 11 23 59_e671498d](https://github.com/user-attachments/assets/7c2fea29-7a9d-4695-a50d-1a743ee860b9)

### Step 1: Node.js Installation

- Update & Upgrade Ubuntu

```bash
sudo apt update && sudo apt upgrade
```
- Install certifications

```bash
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

![WhatsApp Image 2024-09-24 at 23 27 34_9d82a1da](https://github.com/user-attachments/assets/971a956f-3623-4a1e-a9e6-25d5a6d44d96)

- Install Node.js

```bash
sudo apt install -y nodejs
```
![WhatsApp Image 2024-09-24 at 23 42 02_15638cb6](https://github.com/user-attachments/assets/40cf6b3f-72e0-4214-bfb5-61e2ee8adf92)

### Step 2:MongoDB installation
MongoDB stores data in flexible, JSON-LIKE documents. Fields in a database can vary from document to document and data structure can be changed over time. For our example application, we are adding book records to MongoDB that contain book name, ISBN number, author and number of pages.

```bash
sudo apt-get install -y gnupg curl
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
sudo apt-get install -y mongodb-org
```

![WhatsApp Image 2024-09-24 at 23 56 14_9c5109b8](https://github.com/user-attachments/assets/0b48eac8-af15-4f8d-82e9-0281df9b5480)


![WhatsApp Image 2024-09-24 at 23 58 27_f8619a49](https://github.com/user-attachments/assets/62e7370d-013c-4006-ae9b-659777d01a36)

Note: Update the package list before installing mongodb correctly Now, update the package lists from the newly added MongoDB repository.

```bash
sudo apt-get update
```
- Start the MongoDB server:

```bash
sudo systemctl start mongod
```

- Verify that the MongoDB service is up and running:

```bash
sudo systemctl status 
```
![WhatsApp Image 2024-09-25 at 00 04 36_e9249a0e](https://github.com/user-attachments/assets/3c5d2617-e647-4ad2-8399-2fe2be34a5b5)

- Install npm (Node Package Manager):

```bash
sudo apt install -y npm
```

- Install body-parser package

```bash
sudo npm install body-parser
```

![WhatsApp Image 2024-09-25 at 00 12 49_6597cd7a](https://github.com/user-attachments/assets/52a1eec2-622f-4cfb-b0bf-d76891ffdfc1)

- Create a folder named 'Books'

```bash
mkdir Books && cd Books
```

- In the Books directory, Initialize npm projects
 
```bash
npm init
```

- Create a file named ```server.js ```

```bash
sudo nano server.js
```

- Add the following code into the Script block:

```bash
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3300;

// MongoDB connection
mongoose.connect('mongodb://localhost:27017/test', {
    useNewUrlParser: true,
    useUnifiedTopology: true,
})
.then(() => console.log('MongoDB connected'))
.catch(err => console.error('MongoDB connection error:', err));

app.use(express.static(path.join(__dirname, 'public')));
app.use(bodyParser.json());

require('./apps/routes')(app);

app.listen(PORT, () => {
    console.log(`Server up: http://localhost:${PORT}`);
});
```

![WhatsApp Image 2024-09-25 at 12 31 26_f0ba0676](https://github.com/user-attachments/assets/2eca79f8-4ed4-4918-ba25-93164f73bd37)

### Step 3:Install Express and Mongoose:
```bash
sudo npm install express mongoose
```

![WhatsApp Image 2024-09-25 at 00 19 10_2532ad66](https://github.com/user-attachments/assets/98669c22-88fc-45c5-bf1e-9ee12e87f679)

- Create a folder named apps:

```bash
mkdir apps && cd apps
```
- Create a file named routes.js and add the following code:

```bash
const Book = require('./models/book');
const path = require('path');

module.exports = function(app) {
    app.get('/book', async (req, res) => {
        try {
            const books = await Book.find();
            res.json(books);
        } catch (err) {
            res.status(500).json({ message: 'Error fetching books', error: err.message });
        }
    });

    app.post('/book', async (req, res) => {
        try {
            const book = new Book({
                name: req.body.name,
                isbn: req.body.isbn,
                author: req.body.author,
                pages: req.body.pages
            });
            const savedBook = await book.save();
            res.status(201).json({
                message: 'Successfully added book',
                book: savedBook
            });
        } catch (err) {
            res.status(400).json({ message: 'Error adding book', error: err.message });
        }
    });

    app.delete('/book/:isbn', async (req, res) => {
        try {
            const result = await Book.findOneAndDelete({ isbn: req.params.isbn });
            if (!result) {
                return res.status(404).json({ message: 'Book not found' });
            }
            res.json({ message: 'Successfully deleted the book', book: result });
        } catch (err) {
            res.status(500).json({ message: 'Error deleting book', error: err.message });
        }
    });

    app.get('*', (req, res) => {
        res.sendFile(path.join(__dirname, '../public', 'index.html'));
    });
};
```

![WhatsApp Image 2024-09-25 at 00 26 36_9caa98dd](https://github.com/user-attachments/assets/dc579bcc-480f-413d-b77f-18ea23a970a2)


- Create a folder named models:
```bash
mkdir models && cd models
```

- Create a file named ```book.js``` and add the following code nto the script block:

```bash
sudo nano book.js
```

```bash
const mongoose = require('mongoose');

const bookSchema = new mongoose.Schema({
    name: { type: String, required: true },
    isbn: { type: String, required: true, unique: true, index: true },
    author: { type: String, required: true },
    pages: { type: Number, required: true, min: 1 }
}, {
    timestamps: true
});

module.exports = mongoose.model('Book', bookSchema);
```

![WhatsApp Image 2024-09-25 at 00 28 44_579c964d](https://github.com/user-attachments/assets/b912274f-af88-42bd-ab3a-a837a8c6da5b)

### Step 4: Access the Routes with AngularJS

- Change the directory back to Books:

```bash
cd ../... 
```
- Create a folder named public:

```bash
mkdir public && cd public
```

- Add a file named script.js with ```sudo nano script.js``` and paste:

```bash
var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name +
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author +
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
````

![WhatsApp Image 2024-09-25 at 00 37 38_b1a16ffa](https://github.com/user-attachments/assets/5bdbcebb-234d-4019-b49d-ed99a65077d0)

- In public folder create index.html and paste the code into the script block:

```bash
sudo nano index.html
```

```bash
   <!doctype html>
 <html ng-app="myApp" ng-controller="myCtrl">
   <head>
     <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
     <script src="script.js"></script>
   </head>
   <body>
     <div>
       <table>
         <tr>
           <td>Name:</td>
           <td><input type="text" ng-model="Name"></td>
         </tr>
         <tr>
           <td>Isbn:</td>
           <td><input type="text" ng-model="Isbn"></td>
         </tr>
         <tr>
           <td>Author:</td>
           <td><input type="text" ng-model="Author"></td>
         </tr>
         <tr>
           <td>Pages:</td>
           <td><input type="number" ng-model="Pages"></td>
         </tr>
       </table>
       <button ng-click="add_book()">Add</button>
     </div>
     <hr>
     <div>
       <table>
         <tr>
           <th>Name</th>
           <th>Isbn</th>
           <th>Author</th>
           <th>Pages</th>
         </tr>
         <tr ng-repeat="book in books">
           <td>{{book.name}}</td>
           <td>{{book.isbn}}</td>
           <td>{{book.author}}</td>
           <td>{{book.pages}}</td>
           <td><input type="button" value="Delete" ng-click="del_book(book)"></td>
         </tr>
       </table>
     </div>
   </body>
 </html>
 ```
 
![WhatsApp Image 2024-09-25 at 00 39 40_70b85aa2](https://github.com/user-attachments/assets/df943a51-be2b-4325-a54f-290b7d5214ec)


### Step 5: Run the App
Go back to the project root directory and run the following command:

```bash
node server.js
```
![WhatsApp Image 2024-09-25 at 16 59 16_cb46e4a6](https://github.com/user-attachments/assets/669765b1-e241-4093-8510-0c41a89bcda1)

You should now be able to access your Book Register Application by opening a browser and going to http://<your_server_public_ip>:3300

![WhatsApp Image 2024-09-25 at 01 09 17_59a7f004](https://github.com/user-attachments/assets/75f87a3b-c6c9-4c03-a64c-519ff89e30b7)

![WhatsApp Image 2024-09-25 at 17 18 08_67810653](https://github.com/user-attachments/assets/6293dca4-85bf-4693-bee3-d25ada825073)

