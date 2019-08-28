# good coding habit rules


1) destructure and define variables at the top of the function,
then operate on them.

example:

```
getfromApi = item => {
	const {
		id, version
	} = item;
	api.get(
		`someurl.com/api/${id}/${version}`,
		options
	);
}
```
