아래의 명령어로 xcode 설치를 시도했을때
```
 xcode-select --install
```

오류가 뜨면서 제대로 실행되지 않았다.

```
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```


### 해결책
1.  `$ rm -rf /Library/Developer/CommandLineTools`로 오래된 tool들을 제거하고
2.  `$ xcode-select --install` xcode를 재설치한다

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI2MzA5NjEzN119
-->