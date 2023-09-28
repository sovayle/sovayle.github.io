










# RE

### Behind The Scenes

```
      iVar1 = strncmp(*(char **)(in_RSI + 8),"Itz",3);
      if (iVar1 == 0) {
        iVar1 = strncmp((char *)(*(long *)(in_RSI + 8) + 3),"_0n",3);
        if (iVar1 == 0) {
          iVar1 = strncmp((char *)(*(long *)(in_RSI + 8) + 6),"Ly_",3);
          if (iVar1 == 0) {
            iVar1 = strncmp((char *)(*(long *)(in_RSI + 8) + 9),"UD2",3);
            if (iVar1 == 0) {
              printf("> HTB{%s}\n",*(undefined8 *)(in_RSI + 8));
              uVar2 = 0;
```

flag: HTB{Itz_0nLy_UD2}





























