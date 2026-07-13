# MHCnuggets 2.4.0: Keras 3 compatibility patches

## Symptom

Import of `mhcnuggets.src.predict` fails on TensorFlow greater than 2.15 with errors of the form:

```
AttributeError: module 'keras' has no attribute '__version__'
AttributeError: 'Sequential' object has no attribute 'predict_classes'
```

## Root cause

MHCnuggets 2.4.0 was written against the Keras 2 API surface. TensorFlow 2.16+ ships Keras 3 by default, which removes deprecated methods (`predict_classes`) and changes the import path (`tensorflow.keras` versus standalone `keras`).

## Applied patches

Three files in the installed MHCnuggets source tree require modification. After `pip install mhcnuggets==2.4.0`, apply the following edits:

### 1. `mhcnuggets/src/predict.py`

Replace:
```python
from keras.models import load_model
```
with:
```python
from tensorflow.keras.models import load_model
```

Replace all instances of:
```python
model.predict_classes(X)
```
with:
```python
(model.predict(X) > 0.5).astype("int32")
```

### 2. `mhcnuggets/src/models.py`

Replace:
```python
from keras.layers import Input, LSTM, Dense, Embedding, Dropout, GRU
from keras.models import Model, Sequential
from keras.optimizers import Adam
```
with:
```python
from tensorflow.keras.layers import Input, LSTM, Dense, Embedding, Dropout, GRU
from tensorflow.keras.models import Model, Sequential
from tensorflow.keras.optimizers import Adam
```

### 3. `mhcnuggets/src/dataset.py`

Replace:
```python
from keras.utils import to_categorical
```
with:
```python
from tensorflow.keras.utils import to_categorical
```

## Verification

After patching, run:

```python
from mhcnuggets.src.predict import predict
result = predict(class_='I', peptides_path='test_peptides.txt', mhc='HLA-A02:01')
print(result.head())
```

The call should return a DataFrame of predicted IC50 values without errors.

## Automated patch script

An automated patch script is provided at `src/patch_mhcnuggets.py`. Run once after installing MHCnuggets:

```bash
pip install mhcnuggets==2.4.0
python src/patch_mhcnuggets.py
```
