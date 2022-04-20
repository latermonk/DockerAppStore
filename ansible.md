# ansible return code
```
RUN_OK = 0
RUN_ERROR = 1
RUN_FAILED_HOSTS = 2
RUN_UNREACHABLE_HOSTS = 4
RUN_FAILED_BREAK_PLAY = 8
RUN_UNKNOWN_ERROR = 255
```




```
ansible web -i hosts  -m template -a "src=/root/install/autodevops/books/redis.conf dest=/etc/redis/redis.conf"

```
