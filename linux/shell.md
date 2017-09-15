# Examples of Linux commands

## Treat several files at once

* show the number of lines in each file in current directory

    ```
    for file in *; do n=`cat $file | wc -l`; echo "File $file has $n lines"; done
    ```

* rename files in current directory

    ```
    for file in *; do mv $file ${file/temporary/tmp}; done
    ```

* delete several files matching a name

    ```
    find . -type f -name '*~' -delete
    ```

* check differences / matches between two files

    ```
    diff a.txt b.txt | grep "^<"
    diff a.txt b.txt | grep "^>"
    fgrep -xf a.txt b.txt > match.txt
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
