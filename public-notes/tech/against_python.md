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
