# printf debugging
a simple way to debug
* logs are usually placed in `/var/log`
* `log show -last 10s` - show logs on mac
* `logger <text>` to log into the shared log

# debugger
* debuggers can be used via command line (skipping the python's terminal debugger as it's not so much interesting)
* `gdb --args sleep 20` - `gdb` is a common debugger, it shows a lot of details
* `sudo strace ls -l > /dev/null` - trace system calls for `ls -l`, ignoring the `ls`'s output  
* `pyflakes`, `mypy` - static analysis tools for python
* `writegood` - static analysis for English
* 