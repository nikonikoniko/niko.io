its just that everyday actions become difficult.


getting an object attribute when you are not sure it exists

get an attribute from an object if it exists, fill in a default
or from a nested object

```python
        try:
            return operator.attrgetter('owner.name')(obj)
        except:
            return 'something went wrong.'
```

nonetype is an object, wtf is that

```python
    def user(self, obj):
        if hasattr(obj, 'owner'):
            return obj.owner.user_set.all()[0].email
        return ''
```

this throws an error if user is None! this should be a one liner.

show me a better way to do this:

```python
    def products_using_material(self, obj):
        def linkme(id):
            return format_html(
                '<a href="/admin/develop/product/{}/change">{}</a>', id, id)
        return format_html(', '.join([
            linkme(part.assembly.product.id)
            for part in obj.part_set.all()
        ]))
```



this type of stuff:
https://gist.github.com/perrygeo/ee7c65bb1541ff6ac770


---------------------------------

you can't even use the directory structure you want in models because of things like this:

https://github.com/pypa/setuptools/issues/230
https://github.com/pypa/setuptools/issues/230
https://github.com/pypa/pip/issues/3160
most comprehensive on this issue:

https://stackoverflow.com/questions/19602582/pip-install-editable-links-to-wrong-path
two different behaviours for pip depending on some random thing.

please notice this isn't covered anywhere in the official documentation of `setup.py` here:
https://docs.python.org/3.8/distutils/setupscript.html

------------------------------------------------------------

```
In [49]: base64.urlsafe_b64encode(b'hi')
Out[49]: b'aGk='

In [50]: base64.urlsafe_b64decode(b'==========aGk==========')
Out[50]: b'hi'

In [51]: base64.urlsafe_b64decode(b'aGk')
Error: Incorrect padding
```

----------------------------------------------

Inconsistent capitalization and abbreviations

in core:

It makes (a lot) of sense that classes are uppercase, and everything alse is in snake case.

but then between the python keywords there is serious inconsistencies, like `False`

just look at how confusing this list of keywords is, some are abbreviated, some are full words. there might be 'a good reason' behind all of these, but it really reduces the developer experience when you can't apply a consistent rule to the capitalization of things.  if i see `tuple` and `list` as full words, i expect `string` and `boolean` and also `none` instead of `None`


```python

from typing import List

: List[List[tuple]]
list
str
None
bool
False
tuple
dict


```
