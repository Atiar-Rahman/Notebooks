here's clear breakdown of the four main built in collection types in python 
- list
- tuple
- set
- dict

1. list
###### definition: An ordered, mutable(changeable) collection that allows duplicate elements.

```python
my_list = [1,2,3,4,5,'atiar]
```

###### key features
-  ordered(elements have an index)
-  mutable(can add,remove, or change elements)
-  allow duplicates
-  supports slicing and indexing
###### Common methods
```python
my_list.append(5)
my_list.remove(3)
my_list.sort()
my_list.reverse()
```

2.  Tuple
###### Definition: An ordered, immutable collection that allows duplicates.

###### Syntax
```python
my_tuple = (1,2,3,4,5,6,'atiar')
```

###### key features
-  ordered(index able)
-  immutable(cannot be change after creation)
-  allow duplicates
-  often used for fixed data or as dictionary keys

###### Example:
```python
x,y,z = (1,2,3)
```

3.  Set
###### Definition: An unordered, mutable collection of unique elements.

###### syntax
```python
my_set = {1,2,3,4,5,6,7,"atiar"}
```

###### key features
-  unordered(no indexing)
-  mutable (can add, remove elements)
-  No duplicates
-  Useful for  mathematical operations(union,insertion,etc)

###### Example:
```python
my_set.add(4)
my_set.remove(2)
union_set = my_set.union({3, 5})
intersection_set = my_set.intersection({2, 3})

```


4.  Dictionary
###### definition: An unordered collection of key - value pairs. key must be unique and immutable(e.g. strings. numbers,tuples)

###### syntax
```python
my_dict = {'name':'atiar','age':23}
```


###### key features
-  Unordered(python 3.7+ maintain insertion order)
-  keys are values
-  values can be any data type
-  mutable(can add,remove or change pairs)

###### Example:
```python
my_dict['age']=12 # update value
my_dict['country'] = 'Bangladesh' #add key value
del my_dict['age'] # delete a key-value pair

```

##### summary table
|Feature|**List**|**Tuple**|**Set**|**Dictionary**|
|---|---|---|---|---|
|Ordered|✅ Yes|✅ Yes|❌ No|✅ (since Python 3.7)|
|Mutable|✅ Yes|❌ No|✅ Yes|✅ Yes|
|Allows Duplicates|✅ Yes|✅ Yes|❌ No|Keys: ❌ / Values: ✅|
|Indexed Access|✅ Yes|✅ Yes|❌ No|✅ (by key)|
|Syntax Example|`[1,2,3]`|`(1,2,3)`|`{1,2,3}`|`{"a":1,"b":2}`|

