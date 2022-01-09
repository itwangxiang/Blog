# Mac 常用命令


## Mac

### 用户环境变量

- bash

```bash
vim ~/.bash_profile

export ANDROID_HOME=/Users/xxx/Library/Android/sdk
export PATH=${PATH}:${ANDROID_HOME}/tools
export PATH=${PATH}:${ANDROID_HOME}/platform-tools

source .bash_profile
```

- zsh

```bash
vim ~/.zshrc

export ANDROID_HOME=/Users/xxx/Library/Android/sdk
export PATH=${PATH}:${ANDROID_HOME}/tools
export PATH=${PATH}:${ANDROID_HOME}/platform-tools

source .zshrc
```  
