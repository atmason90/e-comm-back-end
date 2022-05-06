# E-Commerce Back-End


GitHub Repository: https://github.com/atmason90/e-comm-back-end 


## Table of Contents

* [Description](#description)  
* [Application Demo](#application-demo)  
* [Usage Instructions](#usage-instructions)  
* [Code Examples](#code-examples)  
* [Technologies Used](#technologies-used)  
* [Questions](#questions)  
* [License](#license)  

## Description

The purpose of this project was to create the back-end of an e-commerce platform. 

This application was built by configuring an Express.js API to use sequelize to interact with a MySql database.

## Application Demo

Link to video demo of this application:  
https://drive.google.com/file/d/1KBD6tlB82vbEWURTLGDzOHshITIDAft2/view?usp=sharing 

## Usage Instructions

To use this application, follow these instructions (Note: must have mysql):
1. Clone this repository to your local machine
2. Navigate to this repository in your terminal and run ```npm install``` to install the necessary dependencies
3. To create the database, enter ```mysql -u root -p``` in your terminal and enter your password. Then in the mysql shell, enter ```source ./db/schema.sql```
4. Exit mysql with ```quit```
5. In your terminal run ```npm run seed``` to seed the database with starter data
6. You can then test the applications routes with a tool such as Insomnia or Postman

## Code Examples

Here is an example of an api route that returns one product by its associated id. This application uses many routes similar to this to execute CRUD processes for products, categories, and tags. 

```js
router.get('/:id', async (req, res) => {
  try {
    const product = await Product.findByPk(req.params.id, {
      include: [Category, {
        model: Tag,
        through: ProductTag,
      }],
    });
    if (!product) {
      res.status(404).json({ message: "That product id does not exist!" });
      return;
    }
    res.status(200).json(product);
  } catch (err) {
    res.status(500).json(err);
  }
});
```

This snippet of code displays how models were created in conjunction with sequelize. the class of Product represents an sql table, wtih id being one of it's columns.

```js
const { Model, DataTypes } = require('sequelize');
const sequelize = require('../config/connection');

class Product extends Model {}

Product.init(
  {
    id: {
      type: DataTypes.INTEGER,
      allowNull: false,
      primaryKey: true,
      autoIncrement: true,
    },
```

## Technologies Used

![JavaScript Badge](https://img.shields.io/badge/Language-JavaScript-yellow)
![Mysql Badge](https://img.shields.io/badge/Database-MySql-informational)
![Node.js Badge](https://img.shields.io/badge/Environment-Node.js-red)
![Express Badge](https://img.shields.io/badge/NPM-Express.js-green)
![Sequelize Badge](https://img.shields.io/badge/NPM-Sequelize-important)
![Dotenv Badge](https://img.shields.io/badge/NPM-dotenv-blueviolet)

## Questions

If you have any questions regarding this project, please reach out to me via email at atmason90@gmail.com.

You can view my other projects on GitHub by visiting my profile. 
[atmason90](https://github.com/atmason90)

## License

MIT License

Copyright (c) 2022 Andrew Mason

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.