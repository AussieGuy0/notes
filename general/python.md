# Python

## Files

### Open files
```python
with open(filename, 'w') as file: # Second param = open type
    # Do Something
```
OR
```python
file = open(filename, 'w')
file.close()
```

**Open Types**
- 'r': File will only be read
- 'w': File will be written to. If file with same name will be deleted (if exists).
- 'a': Append mode. Any data written will be appended to the file.
- 'r+': Combination of 'rw'
- DEFAULT: 'r'

### Write to file
```python
with open(filename, 'w') as file: 
    file.write("lol")
```

### Read from file
```python
with open(filename, 'r') as file: 
    lines = file.readlines()
```

