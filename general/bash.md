# Bash

## If Statement
```bash
str="hello"
if [[ $str == hello ]]
then
    echo "this will print"
else
    echo "this won't print"
fi
```


## Reading file line-by-line

```bash
while read -r line                                                                    
    do
        echo "Text read from file: $line"
    done < "file.txt" # Filename
```

