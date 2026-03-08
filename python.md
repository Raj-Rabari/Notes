```markdown
```python
list = ["abc","def"];
a = 1;


if a < 10 : 
	print('a is less than 10');
elif a > 10 :
	 print('a greater than 10')
else
	print(' a is 10')
	
	
for str in list:
	print(str);
else : 
	print('this will execute after complete execution of for loop or any other loop', 'and it will not execute if loops gets terminated via break statement or return statement');
	
while a < 10 : 
	a = a + 1;

```

`range` function returns object which returns incremented values eventually. you can also give start,stop and step as argument like `range(1,10,2)` => this will generate numbers from 1 to 10 , incremented by 2 and not include 10

```python
for i in range(10) : 
	print(i);

```

## operators

* **arithmatic operators** => `+`,`-`,`*`,`/`,`//`,`%`,`**`
* **comparision operators** => `>`,`<`,`==`,`>=`,`>=`
* **identity operators** => `is` , `is not`
* **logical operators** => `and` , `or` , `not`
* **membership operators** => `in` , `not in`
* **bitwise operators** => `&`,`|`,`^`,`~`
* **bitwise shift operators** => `>>`, `<<`

## python collections

* **List** => ordered, chanagable, allow duplicates
* **tuple** => ordered, unchangable, allow duplicates
* **set** => unordered, can not change existing values, not allow duplicates, unindexed
* **dict** => ordered from python version 3.7, chanagable, no duplicate members

## List :

```python
list1 = [1,"abc","def"];
list2 = list(('abc','def'))
list3 = list1[1:] #slicing like strings

list1[0:2] = [2,"ghi"] # will change first two values
insert(index,value) # will insert at specific index

```