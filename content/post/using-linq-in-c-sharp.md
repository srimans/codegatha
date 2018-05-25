---
author: "Sriman Saswat Suvankar"
date: 2018-05-02
linktitle: LINQ in C#
title: LINQ
tags: ["c sharp","linq"]
topics: ["C Sharp Concepts"]
weight: 10
---

## Introduction

LINQ stands for Language Integrated Query. LINQ helps us in querying objects. Introduction of LINQ is a great advantage for developers because as a developer
if you have ORM(Object Relation Mapping) framework like Entity Framework then you do not need to write SQL queries. Linq can help you query your business objects as well.

LINQ helps to query 

* Objects in memory (Collections)
* Databases (Entities)
* XML
* ADO .NET (DataSets)

## Why Linq?

Internally Linq is converted to SQL when querying databases. As a developer you do not need to switch between writing SQL queries and C# code. Thus it helps in saving time for the developer.
As a result of this the speed of development is very fast. 

When we query databases,we use stored procedures. Code maintainability is an issue with the procs as most of the times you do not know who changed what. There is no version control with the procs. But with the help of Linq we know who changed what and all queries live in a single place i.e inside the project/solution. 
Hence code is properly maintained.

Of course one can argue that stored procs reside on the database server and are precompiled and are faster. Yes that is true. But if we write queries properly then Linq can give effective results. May not be as fast as a proc but almost equal. Hence there is a tradeoff.
Another thing to keep in mind is Linq not only queries entities(databases) but also other three points as written above.

## Syntax

LINQ provides <b>Extension Methods</b> as well as <b>sql alike syntax</b> for querying. Here I will use only Linq extension methods. In one of the examples I will cover how you can write queries with both extension methods and plain queries. Taking you forward I will use only extension methods provided by Linq.
If you are not familiar with extension methods then you can read more about them <a href="/post/how-to-use-extension-methods-in-c-sharp/" target="_blank">here</a>. Ultimately LINQ gives us the power to make us write less code.

Let us consider an object called Vehicle.

`````
  public class Car
  {
      public int Id { get; set; }
      public string Name { get; set; }
      public decimal Price { get; set; }
  }
 `````
 
 Now lets initialize it with come values.
 
 `````
   public Car[] Car => new Car[]
   {
       new Car { Id = 1, Name = "Maruti", Price = 50 },
       new Car { Id = 2, Name = "BMW", Price = 40 },
       new Car { Id = 3, Name = "Audi", Price = 30 },
       new Car { Id = 4, Name = "Chevrolet", Price = 20 },
       new Car { Id = 5, Name = "Hyundai", Price = 50 },
   };
 `````

### Where()
 
 Where helps to filter on a collection based on some condition.
 
 I need to find a list of vehicles that have price greater than or equal to 30
 
 * Without Linq
 
 `````
 var cars = new List<Car>();

 foreach (var car in Cars)
 {
     if (car.Price > 30)
         cars.Add(car);
 }
 `````
 
 * With Linq Extension Methods
 
 By the help of linq its just one line of code.
 
 `````
 Cars.Where(x => x.Price > 30); 
 `````
#### 'x => x.Price > 30' denotes lambda expression. Lambda expression will be covered in a later chapter.
 
 * Without Linq Extension methods
 
 `````
 from car in Cars where car.Price > 30 select car
 `````
 
Its very simple and only one line in this case does the work for us. Moving forward I will use extension methods of linq. You can take it as an exercise to convert all my examples to sql alike syntax. It will be a good practice.

### Select()

Select helps to create your own objects out of the collection you are querying upon. Suppose I want only Name of cars then the syntax would be the following.

`````
var nameOfCars = Cars.Select(x => x.Name);
`````

### Any()

Any says whether any element is there in the sequence or not. If there are no elements then its false else it returns true.Basically it returns a boolean.

<b> No elements is different from null. Any() on a null object will throw an ArgumentNullException </b>.This is because Any() is an extension method.Null is different from empty.For more information read <a href ="https://stackoverflow.com/questions/11538243/why-doesnt-any-work-on-a-c-sharp-null-object" target="_blank">here</a>.
The same principle of null applies to all the extension methods of linq.

I need to find if there is any car whose price is greater than 30.
 
`````
var isAnyCar = Cars.Any(x => x.Price > 30);
`````
 
### All()
 
All() like Any() returns a boolean if all the elements satisfy a given condition else it returns false.

`````
var doesAllCarHavePriceGreaterThanZero = Cars.All(x => x.Price > 0);
`````

### Count()

Count helps to count the number of elements in a collection.So count of cars having price greater than 30 can be written as

`````
var count = Cars.Count(x => x.Price > 30);
`````

### Sum()

Sum can be found out for numeric values. If you try to do Sum() on a non numeric value then you will get a compilation error.

<b>Linq supports chaining of methods. So we can use select and sum to find sum of price of cars.</b>

`````
var priceOfCars = Cars.Sum(x => x.Price);
`````

### First()

It returns the first element of a collection based on conditions. If there is no element then it throws an exception.

I want to fetch one of the cars that has price equal to 50. 

`````
var firstCar = Cars.First(x => x.Price == 50); //Correct
var noFirstCar = Cars.First(x => x.Price > 50); //No car -> Exception
`````

### FirstOrDefault()

It returns the first element of the collection based on the collection. It does not throw exception like First().It returns default value i.e null for reference types and default value for value types(0 for int).

`````
 var firstOrDefault = Cars.FirstOrDefault(x => x.Price == 50); //Correct
 var firstOrDefaultCar = Cars.FirstOrDefault(x => x.Price == 60); //No car -> Default value
`````

It will return null as we do not have any car with price 60. If we would have executed same using first then it would have thrown exception saying <b>'Sequence contains no elements'</b>. 

### Single()

Use Single() only and only when you are pretty sure that you will get only one element. If you are getting more than one or no element in the result set then it will throw exception.

`````
 var onlyOneCar = Cars.Single(x => x.Price == 40); // Correct
 var noCar = Cars.Single(x => x.Price > 50); // No element -> Exception
 var moreThanOneCar = Cars.Single(x => x.Price == 50); // More than one element -> Exception 
`````  

### SingleOrDefault()

If there are no elements in the query result then it returns a default value. i.e null for reference types and default value for value types.If there are more than one element then it throws exception.

`````
 var onlyOneCar = Cars.SingleOrDefault(x => x.Price == 40); // Correct
 var noCar = Cars.SingleOrDefault(x => x.Price > 50); // No element -> Returns default value 
 var moreThanOneCar = Cars.SingleOrDefault(x => x.Price == 50); // More than one element -> Exception 
`````

### Last()

It returns the last element of the collection. If there are no elements then it throws an exception.

`````
var lastCar = Cars.Last(x => x.Price == 30); //Correct
var noLastCar = Cars.Last(x => x.Price > 50); //No element -> Exception
var moreThanOneLastCar = Cars.Last(x => x.Price == 50); //Returns Hyundai car
`````

### LastOrDefault()

It returns the last element of the collection. If there are no elements then it returns default value for value types and reference types respectively.

`````
var lastCar = Cars.LastOrDefault(x => x.Price == 30); //Correct
var noLastCar = Cars.LastOrDefault(x => x.Price > 50); //No element -> Returns default value
var moreThanOneLastCar = Cars.LastOrDefault(x => x.Price == 50); //Returns Hyundai car
`````

Last() returns the last element in the collection.It is just the opposite of First().

These are few basic and important Linq methods.These are convinient,easy and simple to write. Source code can be found <a href="https://github.com/srimans/BlogExamples" target="_blank">here</a>. Thank you for reading the post. Keep visiting for more updates.


 
