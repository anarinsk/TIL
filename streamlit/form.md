# Form 

## Links 

https://twitter.com/andfanilo/status/1453346492605820930
- 틀린 대목이 좀 있지만 고쳐 쓸만 하다. 

https://twitter.com/andfanilo/status/1453346492605820930
- 팔로업 코드 


## What 

- 스트림라이트에서 파라미터의 입력이 끝난 이후 실행을 시키는 방법, form을 알아보자. 

## Why 

- 비동기적 동작이 당연히 되어야 할 것 같은데 그간 되지 않았다. 
- 계산량이 많으면 참 괴롭다. 슬라이드 하다 조정할 때마다 계산이 다시 된다면 사용성과 효율성 모두 손해다. 

## How 

### Without Form 

```py
import streamlit as st
from sklearn import datasets
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split

iris = datasets.load_iris()
X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42
)

if "counter" not in st.session_state: 
    st.session_state.counter = 0 

def _send_data(): 
    st.session_state.counter += 1

st.title("Forms")

# Slide 1

n_estimators = st.slider("Num estimators", 1, 20)
max_depth = st.slider("Max depth", 1, 20)
clf = RandomForestClassifier(n_estimators=n_estimators, max_depth=max_depth)
_send_data()
clf.fit(X_train, y_train)

st.write(f"Your model was trained **{st.session_state.counter}** times :scream:")
```

### With Form 1 

```py
import streamlit as st
from sklearn import datasets
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split

iris = datasets.load_iris()
X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42
)

if "counter" not in st.session_state: 
    st.session_state.counter = 0 

def _send_data(): 
    st.session_state.counter += 1

st.title("Forms")

# Slide 2

- 컨텍스트 매니저를 활용할 때 

with st.form(key="my_form"):
    n_estimators = st.slider("Num estimators", 1, 20)
    max_depth = st.slider("Max depth", 1, 20)
    submit_button_click = st.form_submit_button(label="Rerun")

if submit_button_click:
    clf = RandomForestClassifier(n_estimators=n_estimators, max_depth=max_depth)
    clf.fit(X_train, y_train)
    _send_data()

st.write(f"Your model was trained **{st.session_state.counter}** times :scream:")
```

### With Form 2

```py
import streamlit as st
from sklearn import datasets
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split

iris = datasets.load_iris()
X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42
)

if "counter" not in st.session_state: 
    st.session_state.counter = 0 

def _send_data(): 
    st.session_state.counter += 1

st.title("Forms")

# Slide 2

form = st.form(key="my_form")
n_estimators = form.slider("Num estimators", 1, 20)
max_depth = form.slider("Max depth", 1, 20)

submit_button_click = form.form_submit_button(
    label="Rerun",
    on_click=_send_data
)

if submit_button_click:
    clf = RandomForestClassifier(n_estimators=n_estimators, max_depth=max_depth)
    clf.fit(X_train, y_train)

st.write(f"Your model was trained **{st.session_state.counter}** times :scream:")
```