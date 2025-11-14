
#### Tuto on downloading kaggle datasets on google colab (without importing them locally)

**Step 1**:
```python
! pip install kaggle --quiet
```
**Step 2**:
```python
from google.colab import files
files.upload() # <- opens file explorer
# Create kaggle directory and copy key there
! mkdir ~/.kaggle
! cp kaggle.json ~/.kaggle/
# Change permissions of the file
! chmod 600 ~/.kaggle/kaggle.json
! ls -ltr ~/.kaggle
```
When file explorer opens choose `kaggle.json` file

**Step 3**:
```python
# Import and unzip dataset
! kaggle datasets download -d username/datasetname
import zipfile
with zipfile.ZipFile('/content/satellite-image-classification.zip', 'r') as zip_ref:
  zip_ref.extractall('data') # choose path to unzip data to
```