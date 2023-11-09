---
title: "Rubber Ducky Reviews"
date: 2023-11-08T16:48:55-08:00
draft: false
author: "Carson Webster"
tags:
- Web Development
- Web Framework Reviews
- Devloper Opinion
image: /rubberduckyreviews/ITRubberDucky.jpg
description: "Rubber Ducky Framework Reviews Introduction"
toc: true
---

## Introduction

### The Web's Humble Beginnings
Websites used to be simple. A little birdie once told me that before my time all the internet needed to be was the HTTP compliant to share information written in a simple HTML document. 

### The Simple HTML Era
Just a little bit of:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rubber Ducky Store</title>
</head>
<body>
    <header>
        <h1>Welcome to the Rubber Ducky Store</h1>
    </header>
    <div>
        <div>
            <img src="rubber-ducky1.jpg" alt="Rubber Ducky 1">
            <div>
                <h2>Classic Rubber Ducky</h2>
                <p>$5.99</p>
            </div>
        </div>
        <div>
            <img src="rubber-ducky2.jpg" alt="Rubber Ducky 2">
            <div>
                <h2>Superhero Rubber Ducky</h2>
                <p>$7.99</p>
            </div>
        </div>
        <!-- Add more product listings here -->
    </div>
</body>
</html>
```
would be all you needed to share information about your buisness or hobies with the world. Throw this document on a computer with a simple web server application and badda bing badda boom you just made a website. 

### The Evolution of Web Development
Today though, this simple approach is no longer sufficient. The user expects websites to work as applications with the ability to interact, provide dynamic content, and offer engaging experiences. As web development has evolved, so have the tools, technologies, and frameworks used to build these modern web applications.

Developers are spoiled for choice when when looking for libaries or fameworks to help abstract the complexity of modern web applications. With a handful of solutions for every programming langauge, plus a million more specifically for JavaScript, it is definately a headache finding the development tools that will work the best for your passion project. 

That's why I have decided to experience the headaches for you, and build the same web application in numerous different web frameworks and offer an opinionated grade in numerous tests for each.

## Introducing Rubber Ducky Reviews
The Rubber Ducky Store review project is a versatile and engaging canvas for evaluating the developer experience of various web frameworks. By building the same application with different frameworks, we can directly compare their ease of use, performance, and capabilities. From creating a dynamic front-end to integrating with databases and handling user interactions, this project will showcase how each framework excels and where it may have limitations. Through this hands-on approach, we'll provide a practical and insightful assessment of the unique strengths and weaknesses of each framework, helping developers make informed choices for their own projects. 

### Goals for the Project
The primary goals of the Rubber Ducky Store project are twofold. First, it serves as an enjoyable and lighthearted example application designed to showcase the creative and fun side of web development. Second, it acts as a comprehensive educational tool, allowing us to evaluate and compare various web development frameworks by building the same application. By setting clear evaluation criteria, we aim to provide developers with valuable insights into the strengths, weaknesses, and nuances of different frameworks. My ultimate goal is to empower developers to make informed decisions when selecting a framework for their own projects, all while having a great time exploring the world of web development.

### Target Audience
1. **Web Developers and Programmers**: This is the primary audience interested in web development and software engineering. They may be beginners looking to learn about different web frameworks or experienced developers looking for insights into specific frameworks.
2. **Students**: Those studying web development, computer science, or related fields who want to gain practical insights into building web applications and using various frameworks.
3. **Tech Enthusiasts**: Individuals interested in technology and software development, even if they are not developers themselves. They might enjoy the educational and entertaining aspects of your content.
4. **Employers and Recruiters**: Potential employers or recruiters interested in your skills, passion, and dedication to web development. Your project serves as a portfolio of your work.
5. **Fans and Supporters**: Those who enjoy your content and the lighthearted, engaging approach you take to web development. They might be interested in your journey and enjoy interacting with you.

### Rubber Ducky Store Page Feature List
Here are the features I plan on implementing for each framework. For the framework to be considered feature complete, I should be able to introduce each of the following: 
1. **Static home page**
    - Displays information about the site and funnels the user into the shopping page
2. **Product Listing Page**
    - Displays al ist of rubber duckies for sale with details including name, image, description, and price
    - Categorize duckies for easy browsing
    - Allows users to seach and filter products
3. **Product Details**
    - Provide a dedicated page for each of rubber ducky with additional information and images
4. **Shopping Cart**
    - Allow users to add multiple duckies to their shopping cart
    - Display the cart contents, including item details and total price
    - Enable users to adjust the quantity or remove items
5. **Order Confirmation**
    - Show a confirmation page with order details after mock sucessful purchase
6. **Admin Dashboard**
    - Provide an admin interface to manage product listings, including:
        - Adding
        - Editing
        - Deleting
    - Monitor and manage customer orders

### Wireframe and Mockup
While the baseline site is still underdevelopment, the user interface should not be complex. Here's a simple prototype of what to expect:
![Rubber Ducky Store Prototype](/rubberduckyreviews/storeprototype.png)

### User Flow
Here is how we should expect a user to navigate through the site. Should be very similar to most e-commerce sites. 
#### Homepage
- The user lands on the homepage of the rubber ducky store with information
- A get started button lead's them to the product page
#### Product Details
- On the product page, the user can see:
    - The product's name, image, price, and description
    - An option to add the product to the cart
#### Shopping Cart
- If the user adds a product to their cart, they can:
    - View the cart with a list of items
    - Adjsut the item quantities or remove items
    - Proceed to checkout or continue shopping
#### Checkout
- The user proceeds to the checkout from the shopping cart and:
    - Reviews the order and total price
    - Sees a recipt confirmation with order details
#### Admin Dashboard
- On an admin page, there are controls for:
    - Managing product listings (add, edit, delete products)
    - Monitor and maange customer orders and user accounts

### Technology Stack
For just our little shopping application, we need a few systems set up for this to function. For each framework review, we will be working with: 
1. **A Relational Database** - To store and manage our site data. I will be using [PostgreSQL](https://www.postgresql.org/) for no other reason than it works well and it's what I'm familiar with after a college course.
2. **Deployment** - I expect the web framework to play nice with [Docker](https://www.docker.com/). If the apps server runs next to the databse inside a container running locally on my machine, we'll call that good enough. 
3. **Our Framework Being Reviewed!** I'll explore the options for both front-end and back-end various langages have to offer. 

Here is a list of technologies I am excited to try during this reviewing experiementreviewing experiement: 

- Javascript
    - [Next](https://nextjs.org/)
    - [Nuxt v3](https://nuxt.com/)
    - [SvelteKit](https://kit.svelte.dev/)
- Python
    - [Django](https://www.djangoproject.com/)
    - [Flask](https://flask.palletsprojects.com/en/3.0.x/)
- Ruby
    - [Ruby on Rails](https://rubyonrails.org/)
- PHP
    - [Laravel](https://laravel.com/)
- Java
    - [Spring Boot](https://spring.io/projects/spring-boot)
- Go
    - [Gin](https://gin-gonic.com/)
    - [Echo](https://echo.labstack.com/)
- Rust
    - [Actix](https://actix.rs/)
    - [Rocket](https://rocket.rs/)
    - [Poem](https://github.com/poem-web/poem)
    - [Warp](https://github.com/seanmonstar/warp)
    - [Tide](https://github.com/http-rs/tide)

## My First Review...
First up on the list I plan on reviewing is Sveltekit! It's what I am most familar and comfortable with, making for a solid baseline for our first test. Look forward to the first Rubby Ducky Web Framework Review soon!