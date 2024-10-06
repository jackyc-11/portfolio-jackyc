---
title: L9 - Reactive Frameworks 1
layout: doc
---

# MVC vs MVVM

"It's difficult to truly appreciate what Vue does for us without knowledge of the problems and challenges that web applications have faced in the past and what advantages Vue brings to the table" (*Vue.js in Action* by Hanchett, Listwon). This blog post aims to give a better understanding of some software history by looking at two popular design patterns in software development.

## Model View Controller (MVC)
![](blog_media\mvc.png)
The Model represents the data layer. It manages the business logic, data manipulation, and database interactions. In simple terms, it is responsible for managing the state of the application. (e.g. In a to-do app, the list of to-do items is part of the Model.) 

The View is responsible for displaying the data to the user. It’s the UI, or what the user sees on the screen. The View does not directly reference the Model; it relies on the Controller to get data from the Model. (e.g. The View would display the list of to-do items in the browser.)

The Controller acts as the intermediary between the Model and the View. It takes user input (such as clicks, form submissions, etc.) from user actions in the View, processes that input by interacting with the Model (transforming and routing appropriate events), and updates the View accordingly using data from the model. (e.g. When a user adds a new to-do item, the Controller receives the input, updates the Model, and then refreshes the View to show the new item.)

MVC offers good testability, especially when it comes to unit testing the Model and Controller components. However, testing the View can be more difficult due to its close coupling with the Controller.

Use Cases: Ruby on Rails, Django, ASP.NET, Laravel

## Model View View-model (MVVM)
![](blog_media\mvvm.png)

The Model, similar to the one in MVC, is still the persistent repository for the application's data.

The View, also similar to the one in MVC, is still responsible for displaying information to a user but it's more passive and data-driven.

The ViewModel acts as a binding layer between the Model and the View. The ViewModel receives input from the View, updates the Model, and reflects those changes back in the View through two-way data binding. The data binding exposes data to the View as properties, then View interacts with the data by calling methods that perform actions on the data from the Model, thus easing the process of keeping the UI in sync with the data. Essentially, the ViewModel manages the data flow and logic, while the View remains reactive to any changes in the data.

MVVM improves testability by providing a clearer separation of concerns. The ViewModel can be tested independently from the View and Model because it doesn't directly depend on either. This makes unit testing the ViewModel easier and allows for more focused and thorough tests.

Use Cases: Angular, Vue.js, Xamarin, React

## Vue.js x MVVM

Vue.js mainly supports the MVVM pattern, connecting the View and Model through two way data bindings. This allows developers to link their data directly to the UI with little boilerplate code, making UI development faster and less error-prone. Vue's reactive system (enabled by the ViewModel) makes sure that any change in data automatically reflects in the user interface, reducing the need for manual DOM manipulation.