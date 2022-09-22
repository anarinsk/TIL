## Why 
-  파이썬 혹은 주피터 내에서 필요한 간단한 팁들을 적어보자. 

## Jupyter - 함수 자동 호출 
- 외부에서 정의된 함수를 자동으로 다시 불러오는 기능 

```python
%load_ext autoreload
%autoreload 2
```

## Python - 외부 디렉토리 포함 

- 포함시킬 디렉토리는 하나 상위에 있는 `/functions` 

```python
import sys

if '../functions' in sys.path:
    pass

else:

	sys.path.append('../functions')

#from functions_helpers import *

from functions_instruments import *
sys.path
```

