---
title: "Texamples of using lambda in Python"
collection: teaching
type: "Workshop"
permalink: /teaching/2015-spring-teaching-1
venue: "University 1, Department"
date: 2015-01-01
location: "City, Country"
---

Using lambda to create a simple function:
python

add = lambda x, y: x + y
print(add(3, 5))  # Output: 8

Using lambda to sort a list of dictionaries based on a specific key:

people = [{'name': 'Alice', 'age': 25}, {'name': 'Bob', 'age': 20}, {'name': 'Charlie', 'age': 30}]
sorted_people = sorted(people, key=lambda person: person['age'])
print(sorted_people)  # Output: [{'name': 'Bob', 'age': 20}, {'name': 'Alice', 'age': 25}, {'name': 'Charlie', 'age': 30}]

Using lambda to filter a list based on a condition:

numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # Output: [2, 4, 6, 8, 10]

Using lambda in conjunction with map to transform a list of numbers:

numbers = [1, 2, 3, 4, 5]
squared_numbers = list(map(lambda x: x ** 2, numbers))
print(squared_numbers)  # Output: [1, 4, 9, 16, 25]
