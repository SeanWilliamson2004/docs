---
title: F# exercises
tags: []
description: Beginner F# Exercises Knowledge required Records Unions and "match..
  with" expressions (pattern matching) Functions and type annotations Partial…
created: '2020-08-10'
modified: '2021-12-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Fsharp-exercises.aspx
---

# Beginner F\# Exercises

## Knowledge required

- Records
- Unions and "match.. with" expressions (pattern matching)
- Functions and type annotations
- Partial application
- Function composition and composition operators, including pipes \>\> and \|\>
- Knowledge of functions on lists and IEnumerables including map, fold and reduce

## Exercises

1. Make the following types:
1. Customer which has a name, age and insured item
2. Insured item which is either a Car, a House or Jewellery
3. Car which has a licence number, a year and a model which is either a Ferrari, Ford or Audi
4. A House which has a number of bedrooms and a value
5. Jewellery which has a value

3. Write a function to get an insured item and give back an insurance quote.
1. For cars, its £2000 – 10\* (the current year \- the car's manufactured year) and then \* 2 if it's a ferrari.
2. For house or jewellery, its the value \* 0\.01\.

5. Write a function to get a list of customers and give back the total insurance quotes for all of them
6. Write a function to get a list of customers and give back the total insurance quotes for all of the customers over 50 years old
7. Write a function to take a list of customers and return a tuple of the total insurance quotes for (cars, houses, jewellery)
8. Write a function to do the same as the one above, but only go over each customer in one pass
9. Write unit tests to cover the above, passing example data into the functions in each unit test
