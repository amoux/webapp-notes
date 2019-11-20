# Jinja2 Notes

```python
from jinja2 import Template
```

```python
my_string = "this is a text string to test jinja2"
my_dict = {"string": [s for s in my_string.split()],
           "length": [len(s) for s in my_string.split()]}
my_jsons = [{"name": "ego", "age": 23}, {"name": "leo", "age": 45}]

class MyClass(object):
    def __init__(self, x):
        self.x = x
    def class_method(self):
        return self.x * self.x
    def method_arg(self, y):
        return self.x * y
```

* Passing a single variable:

```python
t = Template("{{ text }}")
print(t.render(text=my_string))
...
'this is a text string to test jinja2'
```

* Iterating items from a list:

```python
t = Template("{% for seqlen in my_list %}{{seqlen}} {% endfor %}")
print(t.render(my_list=my_dict['length']))
...
'4 2 1 4 6 2 4 6'
```

* Iterating items from a list:

```python
print(t.render(my_list=my_dict['string']))
...
'this is a text string to test jinja2'
```

* Iterating items from a dictionary:

```python
t = Template("{% for seqlen in my_list['length'] %}{{seqlen}} {% endfor %}")
print(t.render(my_list=my_dict))
...
'4 2 1 4 6 2 4 6'
```

* Calling a method inside jinja:

```python
t = Template("{{ my_obj.class_method() }}")
print(t.render(my_obj=MyClass(4)))
...
'16'
```

* Calling a method with an argument inside jinja:

```python
t = Template("{{ my_obj.method_arg(2) }}")
print(t.render(my_obj=MyClass(4)))
...
'8'
```

### There is two ways to the same iteration in jinja:

```python
for jsons in my_jsons: print(f"{jsons['name']} is {jsons['age']}.")
...
'ego is 23.'
'leo is 45.'
```

* Using the keys as attributes:

```python
t = Template("{% for jsons in my_jsons %}{{jsons.name}} is {{jsons.age}}. {% endfor %}")
print(t.render(my_jsons=my_jsons))
...
'ego is 23. leo is 45.'
```

* Explicitly using the keys to get the values:

```python
t = Template("{% for jsons in my_jsons %}{{jsons['name']}} is {{jsons['age']}}. {% endfor %}")
print(t.render(my_jsons=my_jsons))
...
'ego is 23. leo is 45.'
```
