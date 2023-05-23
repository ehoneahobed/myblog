---
title: "How to remove the first item in a Python Dictionary"
datePublished: Tue May 23 2023 09:30:39 GMT+0000 (Coordinated Universal Time)
cuid: cli02sz7h01l6banv33kz5iub
slug: how-to-remove-the-first-item-in-a-python-dictionary
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1684789838672/f036d040-d93e-44c5-ab7d-12105833e634.png
tags: python, python3, python-beginner, python-projects, python-dictionaries

---

I was just working on a Python caching system using the first-in-first out (FIFO) policy, when I encountered the challenge of removing the first item in a Python dictionary. My first inclination was to look this up online.

It took me some time to figure it out, so I decided to put together this post so that anyone else looking forward to removing the first item in a Python dictionary can achieve that easily.

Let's get into it. I will first give you the solution and then explain it in an easy-to-understand way for you.

## Remove the first item in a Python dictionary

```python
# Assuming you have a dictionary called my_dict
my_dict = {firstname: 'Obed', surname: 'Ehoneah', age: '99'}

# Get the key for the first item
first_key = next(iter(my_dict.keys()))

# Go ahead an delete the item from the dictionary
del my_dict[first_key]
```

Alternatively, you can use the `pop()` method in place of the `del` function as shown below.

```python
# Assuming you have a dictionary called my_dict
my_dict = {firstname: 'Obed', surname: 'Ehoneah', age: '99'}

# Get the key for the first item
first_key = next(iter(my_dict.keys()))

# Go ahead an delete the item from the dictionary
my_dict.pop(first_key)
```

Now let's get to the explanations.

## What you need to know about Python dictionaries to get this right

Prior to Python 3.7, `dictionaries` were considered unordered sequence of data but there are now considered to be ordered.

However, even though they are ordered, they are not indexable. This means that the data in a Python dictionary does not have an index and therefore cannot be accessed directly with their position in the dictionary.

The ideal way to access any data or item in a Python dictionary will be to use its `key` A dictionary's key plays the same role an index plays in other order sequences like lists and tuples.

Unfortunately there may be times when you need to access a specific data in a certain position of the dictionary while not knowing the key for that particular item. A practical example is what I faced when I was implementing a FIFO caching system with Python dictionary.

I was supposed to check and delete the very first item in the dictionary if the allocated space for the cache (i.e: the number of items to be stored in the dictionary) has been exceeded.

In such a case, I don't know the specific key for the item I would want to delete and therefore I cannot easily delete it.

The solution to this problem is therefore to find a way to get the `key` for the item at position one (or the specific position you are looking for).

I was able to achieve this with the combination of the `next()` function and the `iter()` function.

`first_key = next(iter(my_dict.keys()))`

The `.keys()` when used on a Python dictionary, returns a view object of the keys of that dictionary.

The `iter()` function is a built-in Python function that returns an iterator object. When used on the keys of the dictionary, it turns them into an iterator which makes them behave like the common iterators (ie: lists and tuples).

This gives them an order and kind of index them such that you can move from one key to the other with the help of the `next()` function.

When called for the first time, the `next()` function will give us the first key. So, if you are looking for a specific position in the dictionary then you would have to know how many times to run the `nex()` function in order to get it.

In this example, we are interested in only the first position so we only call `next()` once and we get the key for the first item.

## Conclusion

I hope you found this article useful. I create a lot of software engineering content on various platforms and share daily motivation for software engineers on Twitter. I also love connecting with people who are determined to make an impact on the world. If you are one of such people, let's connect on [Twitter](https://ehoneahobed.com/twitter).

You may also want to follow me on various platforms to get access to the wonderful content that I keep creating regularly:

* YouTube: [https://ehoneahobed.com/youtube](https://ehoneahobed.com/youtube)
    
* Linkedin: [https://ehoneahobed.com/linkedin](https://ehoneahobed.com/linkedin)
    
* Newsletter: [https://techpady.substack.com](https://techpady.substack.com)
    
* Discord Server: [https://techpady.com/discord](https://techpady.com/discord)
    
* Twitter: [https://ehoneahobed.com/twitter](https://ehoneahobed.com/twitter)