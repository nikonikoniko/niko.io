2) lack of types, variable naming schemes

### singular NOUN = object

for example

```
const material = {};
const incident = {};
```

### plural NOUN = array of objects, describing the objects inside

```
const materials = [{}, {}];
const incidents = [{}, {}];
```

### adjective = Bool

```
const valid = true;
const person.tall = false;
```

this allows for nice to read code such as

```
if (person.tall) {
	greet('hows the weather up there?')
}
```
