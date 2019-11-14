# data relationships

if it is a named relationship, do not be afraid to name ii

```python
class Material(Model):
	...
	raw_material_step = models.ForeignKey('ProductionStep')
	# related_name 'steps'
	...


class Leather(Material):
	...
	tanning_step = models.ForeignKey('ProductionStep')
	other_leather_step = models.ForeignKey('ProductionStep')
	# related_name 'steps'
	...


class MaterialProductionStep(Model):
	...
	material = models.ForeignKey(Material, related_name='steps')
	...
```
