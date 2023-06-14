---
title: "Entity Component Systems Introduction"
date: 2023-06-13T09:56:43-07:00
draft: false
author: "Carson Webster"
tags: 
- Bevy ECS
- Rust
- Functional programming
- Objected orientated programming
image: /SlugECS/ECSImage.png
description: "A glimpse into Entity Component Systems, With a Bevy of Slugs"
toc: true
---
During my last year in college, I was privileged enough to research and present a technical topic to my peers. Since I have all the research done, I'll also share my findings here. 

## What is ECS?
Entity-Component-System (ECS) architecture is a relatively new software design pattern that has gained widespread popularity in the gaming and simulation industry due to its flexibility and performance benefits. ECS separates an object’s data and behavior into two distinct components: entities and components. An entity is an object in the game world, while a component is an attribute or behavior of that entity. This architecture provides a framework for managing these entities and components, allowing for a more efficient and organized development process.

ECS offers several advantages over other software design patterns. Firstly, ECS architecture allows for easy modification and extension of code, which is crucial for game development where requirements are constantly changing. Secondly, ECS offers better performance than other design patterns due to its focus on data-oriented design, which allows for better memory usage and cache locality. Thirdly, ECS architecture favors composition over inheritance, allowing for greater flexibility by defining an entity by its traits rather than using a fixed inheritance tree.

## Entity Component Systems Motivation
ECS arose from developer's frustration with the object orientated model. If you're unfamiliar with this programming approach, it's largely explained with a root object or class with basic functionality being inherited by sub modules or sub classes with additional functionality added on top from the base module or class. This approach is commonly used in `C++`, `Java`, `Javascript/Typescript`, and sometimes `Python`, among others. This approach of class inheritance while useful in many programs, could create restrictions and headaches as the program / video game / simulation grows more complex. 

Take this example:
![Animal OOP example](/SlugECS/hierarchy.png)

In this picture, `Thing` is a base class that has default functionality expected to be shared with all inherited classes. Each other class represents a thing that exists in the game or simulation. The `Rock`, `Mammal`, `Bird`, `Fish` all are program entities that inherit from the base thing functionality, and add additional behavior specific to it's role. 

Furthermore, the `Dog` inherits from the functionality introduced by the `Mammal` class, and the `Duck` inherits functionality introduced by the `Bird` class.

The problem now lies with how we introduce the `Platypus` class to our program. This abnormal animal has traits that are exclusive to the `Mammal` class, like having fur, and traits that could NOT be included by the `Mammal` class, like laying eggs. 

If the programmer wishes to introduce a class that requires traits or behaviors defined in two different classes, the programmer must choose one class to inherit from and duplicate the remaining code. 

This example was heavily inspired by [this youtube video by Dylan Falconer](https://www.youtube.com/watch?v=s6TMa33niJo). Check out the first minute of his for another example. 

Can ECS solve this problem and more? Let's dive in to this new programing paradigm.

## Entity, Components, and Systems
Three words, three concepts, three tools that have the ability to flexibly and efficiently conjure any digital world when combined. Let's take a look at each of them:

### Entities
- Represent all of our `things` in our program. A `thing` in a program is whatever you need it to be. 
	- A rock
	- player
	- health bar
	- or arrow fired from a bow.
- All represented by a single numerical ID #.

### Components
- Are the `data` we attach to our entities.
- It's a `structure` that holds one or many data types.
- Data types attached to an entity could be any primitive or defined type. For example, maybe a:
	- `Position(int x, int y)`
	- `Damage(float)`
	- `On_Ground(bool)`

### Systems
- Functions that are run to query and mutate components.
- The logic of the program. Defines how an entities components will change over time.
- Just a regular plain ol' function! Has the ability to query entities and change it's component data: 
	- `fn update_position(enemies)`

## How does ECS work?
Conceptually, think of a table containing all the entities as rows and attached components as a boolean in a column. Like so:
![ECS Table Example](/SlugECS/ECStable.png)

This large `Hash Table` is central to how ECS functions. When determining which data components are attached to which entities, this table is referenced. 

The `key` in this hash table, is the entity id, and returns a stored `integer` value. For example:
- Ecs_Table[2] = 5 base10 OR 101 base2

By looking at the binary representation of this returned integer, an ECS engine has the ability to `bit index` and determine true or false values representing attached components. 

In this table, reading from right to left, the first bit represents T/F for `on_ground` component, then T/F for `damage` component, and lastly T/F for `position` component for the most significant bit. 

This bit indexing strategy is how `systems` can quickly query the `components` attached to a entity to `modify` the associated data according to the logic in an active game state. 

## A Small Example
So far this post has admittedly been a lot of definitions and theory. While I think this jibber jabber is fascinating, I created a small example anyone could get behind. 

The following example is written in [Rust](http://rust-lang.org) using the [Bevy ECS Library](https://bevyengine.org/). While these are the tools I used to implement an ECS program, I am not going in-depth on the specifics of using the Bevy ECS library with rust. Only a small amount of Rust evangelism will be present going forward, expect a future post where I detail the aspects I love about the Rust language. 

### The Slug Vending Machine
Let’s pretend we are writing a program that simulates pulling a random sticker from one of those quarter vending machines.

![Slug Vending Machine Image](/SlugECS/SlugMachine.png)

In our vending machine exists three variants of Sammy the Slug we can receive.

Before each program run, spawn a Slug entity with a random variant. 

During the execution, print the random slug that was spawned.

#### Components we'll need
![Slug Component](/SlugECS/SlugComponent.png)

Remember that entities are just a number. An entity can thought of being defined by the components we attached to them. To create a slug sticker in our game, we define a `Slug` component. An entity in our game is considered a slug if they have the `Slug` component attached.

Also remember that components are a structure that holds one or more other data types. Here, the `Slug` component requires the additional components `Slug_type` and `Value` which we'll define below.

![Slug Component](/SlugECS/SlugTypeComponent.png)

Here, the `SlugType` component is an `Enumeration`, not a `Structure`. This is similar to a structure, but it's a rust specific convention for crating custom `Types`. This `SlugType` component can be attached to an entity or included in another component, and is either one of three types: `Fiat`, `Grateful`, or `Strong` exclusively. 

![Slug Component](/SlugECS/ValueComponent.png)

Lastly, a `Value` component is defined and set to hold a `float` value. This float value represents... The value the slug sticker is worth of course! $\$\$

#### Our Game Logic As Systems
##### Spawning the slug sticker
![Spawn Random Slug Image](/SlugECS/SpawnRandomSlugSystem.png)

Here is our first example of a `System` that can interact with our entities and their attached components. In this `spawn_random_slug` function, we use the commands given as a parameter to spawn an entity with a `Slug` component attached. Remember that each slug component requires a `SlugType` and `Value` component as well. 

The `slug_type` variable is assigned by generating a random number and using the modulo operator to bind it between 0 and 2. The next strange syntax is a fancy functional programming concept called `Pattern Matching`! Essentially it's short hand for multiple case statements, where each case is required to be included. Based on the random number, a `SlugType` enumeration value is assigned to the variable.

The `value` variable is assigned based off what type the `slug_type` was assigned to. Again, a fancy pattern matching statement is used to assign the `value` variable to a `Value` component, whose float is determined by the arm of the pattern match. 

With a `Slug_Type` and `Value` finally decided, we can spawn a new entity with the `Slug` component!

##### Printing the slug sticker
![Print Our Slug System](/SlugECS/PrintSlugsSystem.png)

This `print_my_slugs` function handles displaying which slug sticker was spawned into our world from the previous system. As a parameter, the variable `query` is requested of type `Query<&Slug>`. This is a Bevy specific way of grabbing a list of all entities, filtered down to those with the `Slug` component. 

With our slug stickers in hand, we print them out to the user. Again, we use another pattern matching statement against it's `slug_type` and call the `print` rust macro with a nice statement and it's variable `value`. Notice that the print statement changes in the different pattern match arms, especially the strong find which is a rare find!

##### Running the program
Lastly, let's call our systems in the main function and see it's output:
![Main function example](/SlugECS/MainFunction.png)

![Running example where fiat sticker is pulled](/SlugECS/RunFiat.png)

![Running example where grateful sticker is pulled](/SlugECS/RunGrateful.png)

## ECS Poster
![alt](/SlugECS/ECSposter.png)

## ECS Literature Exploration
Link to my literature review of different experimental ECS programs:
[CarsonWebster Entity Component Systems Final Review](/SlugECS/ccwebste_Entity_Component_Systems_Final_Project.pdf)

## References and Shoutouts
- Read the source code for this example at [https://github.com/CarsonWebster/slug_ecs/](https://github.com/CarsonWebster/slug_ecs/)
- [Bevy Cheet Book](https://bevy-cheatbook.github.io/programming/ecs-intro.html)

- [What is an ECS? feat. Bevy and Rust](https://www.youtube.com/watch?v=AirfWcVOEHw)

- [Entity Component System (ECS) - Definition and Simple Implementation](https://www.youtube.com/watch?v=s6TMa33niJo)
