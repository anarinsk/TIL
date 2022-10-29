# numpy 성능 체크 

```
import numpy as np
size_of_mat = 2**14
X = np.random.randn(size_of_mat, size_of_mat).astype(np.float32)
out = np.empty_like(X)
%timeit np.dot(X.T, X, out=out)
```
