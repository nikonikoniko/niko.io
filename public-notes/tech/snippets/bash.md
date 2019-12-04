search and replace in directory:

```
find ./ -type f -exec sed -i 's/string1/string2/' {} \;
```


then something else


expose a docker container or local port on local networks

```
socat tcp-listen:80,reuseaddr,fork tcp:172.18.0.1:8000
```
