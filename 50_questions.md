
# 🐚 Top 50 Shell Scripting Interview Questions and Answers for DevOps Engineers

## 📘 Basics

1. **What is a shell? How is it different from a terminal?**  
   A shell is a command-line interpreter that provides a user interface for accessing the operating system's services. A terminal is an interface that lets you interact with the shell.

2. **How do you write and execute a basic shell script?**  
   Create a file with `.sh` extension, add `#!/bin/bash` at the top, write commands, then run:  
   ```bash
   chmod +x script.sh
   ./script.sh
   ```

3. **What is the difference between `sh` and `bash`?**  
   `sh` is the Bourne shell; `bash` is the Bourne Again Shell with more features like arrays, `[[ ]]`, improved scripting constructs.

4. **How do you pass arguments to a shell script?**  
   ```bash
   ./script.sh arg1 arg2
   echo $1 $2
   ```

5. **Explain the meaning of `$0`, `$1`, `$@`, `$*`, and `$#`.**  
   - `$0`: Script name  
   - `$1`, `$2`...: Positional parameters  
   - `$@`: All arguments as separate strings  
   - `$*`: All arguments as a single string  
   - `$#`: Number of arguments

6. **What are environment variables? How do you access them?**  
   Key-value pairs in the environment. Access with `$VAR_NAME`, set with `export VAR=value`.

7. **What does `#!/bin/bash` do?**  
   It's a shebang that tells the system to use Bash to interpret the script.

8. **How do you make a script executable?**  
   ```bash
   chmod +x script.sh
   ```

9. **What’s the difference between `source script.sh` and `./script.sh`?**  
   `source` runs the script in the current shell. `./` runs it in a new subshell.

10. **How do you read user input in a shell script?**  
    ```bash
    read -p "Enter your name: " name
    echo "Hello, $name"
    ```

## 🔁 Flow Control

11. **How do you write `if-else` and `case` statements in bash?**  
    ```bash
    if [ $a -gt 0 ]; then
      echo "Positive"
    else
      echo "Negative"
    fi
    ```

    ```bash
    case $var in
      1) echo "One";;
      2) echo "Two";;
      *) echo "Other";;
    esac
    ```

12. **What’s the difference between `[` and `[[` in conditionals?**  
    `[[` is more powerful and safer (supports pattern matching, no pathname expansion).

13. **How do you use `&&` and `||` in condition checking?**  
    - `cmd1 && cmd2`: cmd2 runs only if cmd1 succeeds.  
    - `cmd1 || cmd2`: cmd2 runs only if cmd1 fails.

14. **Explain the use of `while`, `for`, and `until` loops in shell scripts.**  
    ```bash
    for i in 1 2 3; do echo $i; done
    while [ $x -lt 5 ]; do ((x++)); done
    until [ $x -ge 5 ]; do ((x++)); done
    ```

15. **How do you break out of a loop or skip iterations?**  
    - `break`: exits the loop  
    - `continue`: skips to the next iteration

## 🔨 Script Functions & Operations

16. **How do you define and call functions in a shell script?**  
    ```bash
    function greet() { echo "Hello $1"; }
    greet World
    ```

17. **How do you return values from a function?**  
    Use `return` for numeric exit codes or `echo` for strings:
    ```bash
    function get_name() { echo "DevOps"; }
    name=$(get_name)
    ```

18. **What are exit codes and how do you use them?**  
    `0` = success, other numbers = errors. Access last exit code via `$?`.

19. **What is the significance of `set -e`, `set -u`, and `set -x`?**  
    - `set -e`: Exit on error  
    - `set -u`: Error on unset variables  
    - `set -x`: Print each command before executing

20. **How do you handle errors in bash scripts?**  
    Use `trap`, `set -e`, conditional checks, and logging.

## 🧹 File & Directory Operations

21. **How do you check if a file exists and is readable/writable/executable?**  
    ```bash
    if [ -f file.txt ]; then echo "Exists"; fi
    ```

22. **How do you loop over a list of files in a directory?**  
    ```bash
    for f in *.txt; do echo "$f"; done
    ```

23. **How do you count the number of lines/words/characters in a file?**  
    ```bash
    wc -l file.txt
    wc -w file.txt
    wc -c file.txt
    ```

24. **How do you rename or move multiple files using a shell script?**  
    ```bash
    for f in *.txt; do mv "$f" "${f%.txt}.bak"; done
    ```

25. **Write a script to find and delete files older than 30 days.**  
    ```bash
    find /path -type f -mtime +30 -exec rm {} \;
    ```

## 📊 String and Text Processing

26. **How do you extract substrings in bash?**  
    ```bash
    str="DevOps"
    echo ${str:0:3}
    ```

27. **How do you use `cut`, `awk`, `sed`, and `grep` in scripts?**  
    ```bash
    cut -d':' -f1 /etc/passwd
    awk '{print $1}' file.txt
    sed 's/foo/bar/' file.txt
    grep "pattern" file.txt
    ```

28. **How do you replace a string in a file using a shell script?**  
    ```bash
    sed -i 's/old/new/g' file.txt
    ```

29. **How do you process CSV or log files in bash?**  
    ```bash
    IFS=',' read -r a b c < file.csv
    ```

30. **How do you convert all filenames in a folder to lowercase?**  
    ```bash
    for f in *; do mv "$f" "$(echo $f | tr '[:upper:]' '[:lower:]')"; done
    ```

## 🔐 Permissions and Execution

31. **How do you check if a script is running as root?**  
    ```bash
    if [ "$EUID" -ne 0 ]; then echo "Run as root"; exit 1; fi
    ```

32. **How do you schedule a shell script using `cron`?**  
    ```bash
    crontab -e
    */5 * * * * /path/to/script.sh
    ```

33. **What is `chmod +x` and why is it necessary?**  
    Grants execute permissions to a script file.

34. **How do you run a script in the background and monitor it?**  
    ```bash
    ./script.sh &
    tail -f logfile.log
    ```

35. **How do you kill a running process from a script?**  
    ```bash
    pkill -f script.sh
    ```

## 📡 Networking and Services

36. **How do you check if a port is open on a remote host?**  
    ```bash
    nc -zv host port
    ```

37. **Write a script to check the status of a systemd service.**  
    ```bash
    systemctl is-active nginx
    ```

38. **How do you download a file using `curl` or `wget` in a script?**  
    ```bash
    curl -O http://example.com/file
    wget http://example.com/file
    ```

39. **How do you test if a website is reachable from a script?**  
    ```bash
    curl -s --head http://example.com | head -n 1
    ```

40. **Write a script to perform health checks on microservices.**  
    ```bash
    for url in "http://service1/health" "http://service2/health"; do
      curl -s $url | grep "UP" || echo "$url is down"
    done
    ```

## 💾 System & Disk Monitoring

41. **How do you get system uptime, memory usage, and disk usage?**  
    ```bash
    uptime
    free -h
    df -h
    ```

42. **Write a script to alert when disk usage exceeds 80%.**  
    ```bash
    df -h | awk '$5+0 > 80 {print $0}'
    ```

43. **How do you monitor CPU usage using a shell script?**  
    ```bash
    top -bn1 | grep "Cpu"
    ```

44. **How do you check running processes in a script?**  
    ```bash
    ps aux | grep nginx
    ```

45. **How do you send email notifications from a bash script?**  
    Use `mail`, `sendmail`, or integrate with tools like `msmtp`.

## 🧪 Debugging and Best Practices

46. **How do you debug a shell script line by line?**  
    Add `set -x` or run with `bash -x script.sh`.

47. **How do you log output and errors to a file?**  
    ```bash
    ./script.sh > output.log 2>&1
    ```

48. **What are traps in bash and how do you use them?**  
    Traps catch signals (e.g. `EXIT`, `INT`) and run cleanup commands.

49. **How do you ensure your script is safe and idempotent?**  
    Add checks before actions, avoid hard deletes, log all actions, use retries.

50. **What are some best practices for writing maintainable shell scripts?**  
    - Use comments  
    - Handle errors  
    - Modularize with functions  
    - Avoid hard-coded values  
    - Use descriptive variable names  
