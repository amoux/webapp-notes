.. code:: ipython3

    from jinja2 import Template

.. code:: ipython3

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

.. code:: ipython3

    # Passing a single variable:
    t = Template("{{ text }}")
    print(t.render(text=my_string))


.. parsed-literal::

    this is a text string to test jinja2


.. code:: ipython3

    # Iterating items from a list:
    t = Template("{% for seqlen in my_list %}{{seqlen}} {% endfor %}")
    print(t.render(my_list=my_dict['length']))


.. parsed-literal::

    4 2 1 4 6 2 4 6 


.. code:: ipython3

    # Iterating items from a list:
    print(t.render(my_list=my_dict['string']))


.. parsed-literal::

    this is a text string to test jinja2 


.. code:: ipython3

    # Iterating items from a dictionary:
    t = Template("{% for seqlen in my_list['length'] %}{{seqlen}} {% endfor %}")
    print(t.render(my_list=my_dict))


.. parsed-literal::

    4 2 1 4 6 2 4 6 


.. code:: ipython3

    # Calling a method inside jinja:
    t = Template("{{ my_obj.class_method() }}")
    print(t.render(my_obj=MyClass(4)))


.. parsed-literal::

    16


.. code:: ipython3

    # Calling a method with an argument inside jinja:
    t = Template("{{ my_obj.method_arg(2) }}")
    print(t.render(my_obj=MyClass(4)))


.. parsed-literal::

    8


.. code:: ipython3

    # There is two ways to the same iteration in jinja:
    for jsons in my_jsons: print(f"{jsons['name']} is {jsons['age']}.")


.. parsed-literal::

    ego is 23.
    leo is 45.


.. code:: ipython3

    # Using the keys as attributes:
    t = Template("{% for jsons in my_jsons %}{{jsons.name}} is {{jsons.age}}. {% endfor %}")
    print(t.render(my_jsons=my_jsons))


.. parsed-literal::

    ego is 23. leo is 45. 


.. code:: ipython3

    # Explicitly using the keys to get the values:
    t = Template("{% for jsons in my_jsons %}{{jsons['name']}} is {{jsons['age']}}. {% endfor %}")
    print(t.render(my_jsons=my_jsons))


.. parsed-literal::

    ego is 23. leo is 45. 


