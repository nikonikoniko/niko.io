## Undefined variable in flask template

for flask error, which is a 500 error when the template calls an undefined variable

```
jinja2.exceptions.UndefinedError: 'dict object' has no attribute 'xxx'
```

if you are working with dynamic data, you might want the jinja template rendering to fail silently.  It might be expecting a value that is not set, but you don't want it all to fail because of it.

solving this is:

```python
from jinja2 import Undefined, Template, Environment

from flask import (
    Flask,
    request,
    render_template,
    json,
)

class SilentUndefined(Undefined):
    def _fail_with_undefined_error(self, *args, **kwargs):
        return
app = Flask(__name__, template_folder='../templates/')

app.jinja_env.undefined = SilentUndefined
```

now you can reference variables that don't exist.
