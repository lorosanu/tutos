# Examples of Linux commands

## Process several files at once

* show the number of lines in each file in current directory

    ```
    for file in *; do n=`cat $file | wc -l`; echo "File $file has $n lines"; done
    ```

* rename files in current directory

    ```
    for file in *; do mv $file ${file/temporary/tmp}; done
    for filename in *; do mv $filename unix_$filename; done
    for file in `ls */default_*`; do mv -i $file ${file/default_/}; done
    ```

* create new files by changing names and content of other files

    ```
    for file in multilabel*; do sed 's/multilabel/multiclass/g' $file > ${file/multilabel/multiclass}; done
    ```

* delete several files matching a name

    ```
    find . -type f -name '*~' -delete
    ```

## Comparing two files

* check equality

    ```
    diff -q <(sort file1.txt) <(sort file2.txt)
    echo $?
    1

    diff -q <(sort file1.txt) <(sort file1.txt)
    echo $?
    0
    ```

* unique intersection

    ```
    sort file1.txt file2.txt | uniq -d
    ```

* intersection

    ```
    fgrep -xf file1.txt file2.txt
    ```

* exclusive union

    ```
    sort -u file1.txt file2.txt
    ```

## Fields in file

* display last field on each line in file (default whitespace delimiter)

    ```
    awk '{print $NF}' dictionary.txt
    ```

* display the second last field on each line in file (having ':' delimiters)

    ```
    awk -F':' '{print $(NF-1)}' dictionary.txt
    ```

* display the number of fields on each line in file

    ```
    awk '{print NF}' dictionary.txt
    ```

* check to see if file has the same number of fields on each line

    ```
    awk '{print NF}' dictionary.txt | uniq
    ```

## Files and folders

* display list of sub-folders in current folder

    ```
    ls -l | grep "^d"
    ls -l | grep "^d" | awk '{print $NF}'
    ```

* get the name of the largest file in current folder

    ```
    ls -al | grep "^-" | sort -r | head -n 1 | awk '{print $NF}'
    ```

* read file line by line

    ```
    while read -r line
    do
        echo $line
    done < file.txt
    ```

## String processings

* upcase

    ```
    s="TestString"
    echo ${s^^}
    TESTSTRING
    ```

* delete last character

    ```
    s="TestString"
    echo ${s::-1}
    TestStrin
    ```

* left align text on 20 characters

    ```
    s="TestString"
    printf "%-20s |\n" "$s"
    TestString           |
    ```

* right align text on 20 characters

    ```
    s="TestString"
    printf "%20s |\n" "$s"
              TestString |
    ```

* check if string contains substring

    ```
    s="TestString"
    if [[ $s = *"est"* ]]; then echo "true"; else echo "false"; fi
    true
    if [[ $s =~ "est" ]]; then echo "true"; else echo "false"; fi
    true

    if [[ $s = *"esT"* ]]; then echo "true"; else echo "false"; fi
    false
    if [[ $s =~ "esT" ]]; then echo "true"; else echo "false"; fi
    false
    ```
* check if string contains digits

    ```
    s="TestString"
    if [[ $s =~ \d ]]; then echo "true"; else echo "false"; fi
    false
    if [[ $s =~ [[:digit:]] ]]; then echo "true"; else echo "false"; fi
    false

    s="test-digits-21"
    if [[ $s =~ \d ]]; then echo "true"; else echo "false"; fi
    true
    if [[ $s =~ [[:digit:]] ]]; then echo "true"; else echo "false"; fi
    true
    ```

* check if string contains only digits

    ```
    s="TestString"
    if [[ $s =~ [^[:digit:]] ]]; then echo "false"; else echo "true"; fi
    false

    s="231654"
    if [[ $s =~ [^[:digit:]] ]]; then echo "false"; else echo "true"; fi
    true
    ```

* split string by '-' and process one item at a time

    ```
    s="test-split-string"
    table=(${s//-/ })
    for item in "${table[@]}"
    do
      echo $item
    done
    test
    split
    string
    ```

## Archives

* create

    ```
    tar -C examples/ -czf examples.tar.gz .
	tar -C examples/ -cjf examples.tar.xz .
    ```

* view content

    ```
    tar -tf examples.tar.gz
    tar -tf examples.tar.xz
    ```

* extract

    ```
    tar -xzf examples.tar.gz
    tar -xjf examples.tar.xz
    ```

## Disk memory usage

```
df -h
du -hs
du -h -L --max-depth=1
```

## Scheduler

```
crontab -e

# every 2 minutes
*/2 * * * * rm -rf ~/.errors*

# every hour
@hourly rm -rf ~/.errors*
0 */1 * * * rm -rf ~/.errors*
```

## Screens

* list all screens

    ```
    screen -ls
    ```

* create screen named 'exp'

    ```
    screen -S exp
    ```

* reattach to screen 'exp' (or create it if it doesn't exist)

    ```
    screen -R exp
    ```

* kill screen "exp" (execute command 'quit' in the session 'exp')

    ```
    screen -S exp -X quit
    ```

* shortcuts within screen
	- CTRL+a c : new window
	- CTRL+a n : next window
	- CTRL+a p : previous window
	- CTRL+a d : detach screen from terminal
