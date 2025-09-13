[ usefull functions / tricks :] ]
1. **enumerate**(*iterable*)
      - adds a counter (index, starting from 0) to each item in a list or any other iterable [usefull when indexing through dictionares and needing locations of certain keys]
      
      In:
      ```python
      my_list = ['var1', 'var2', 'var3']

      for index, var in enumerate(my_list):
      print(f'index {i} : {var}')
      ```
      Out:
      ```python
      index 0: var1
      index 1: var2
      index 2: var3
      ```
      - version with dictionary:
      ```python
      for i, (k, v) in enumerate(example_dict.items()):
            print(i, k, v)
      ```

      <br>
2. **islice()** 
      - returns only certain nums of values from dictionary (slices it)
      
      In:
      ```python
      from itertools import islice  

      my_dict = {'a': 1, 'b': 2, 'c': 3, 'd': 4}  
      num_of_items = 2  
      left_values = dict(islice(my_dict.items(), num_of_items))  
      print(left_values)
      ```
      Out:
      ```python
      {'a': 1, 'b': 2}
      ```
<br>

3. **skip** a certain value while iterating using **range()** function
      - ex. print anything but 50
      ```python
      for i in [x for x in range(100) if x != 50]:
        print(i)
      ```

4. get value from dictionary by it's index
      ```python
      my_dict = { 'val1': 1,
                  'val2': 2,
                  'val3' : 3 }

      first_value = list(iter(my_dict.values()))[0]
      second_value = list(iter(my_dict.values()))[1]
      ```