###12.4的第2题：试分析ucore操作系统内核是如何把子进程exit()的返回值传递给父进程wait()的？
子进程调用do_exit函数设置exit_code

```
current->state = PROC_ZOMBIE;
current->exit_code = error_code;
```

父进程调用do_wait函数将子进程的exit_code存入code_store

```
found：
    if (proc == idleproc || proc == initproc) {
        panic("wait idleproc or initproc.\n");
    }
    if (code_store != NULL) {
        *code_store = proc->exit_code;
    }
```
