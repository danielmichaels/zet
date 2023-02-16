# reproducible random strings in python

```python
import hashlib
import uuid

seed = 'Type your seed_string here' #Read comment below

m = hashlib.md5()
m.update(seed.encode('utf-8'))
new_uuid = uuid.UUID(m.hexdigest())
```

I used this to create kube resources programatically whilst keeping
their names consistent for easier deletion and management.

Tags:

    #python #kubernetes

