---
title: Mac 下修改 caps lock 键功能

---

偶然发现 <kbd>ctrl</kbd> 作为修饰键在文本编辑中的强大作用，然而按该键与其它键组合非常不方便，很别扭，于是将之与 <kbd>caps lock</kbd> 互换。后来一直心水 vim 的强大功能，同样有一个问题，vim 中高频率使用的 <kbd>esc</kbd> 也很不好按，网上流行的做法也是将之与 <kbd>caps lock</kbd> 互换。原本以为这是一个冲突，最近突然发现这是可以共存的，<kbd>caps lock</kbd> 可以同时替代两个键的功能，即单独按下时是 <kbd>esc</kbd> ，与其它键组合时是 <kbd>ctrl</kbd> 。以下记录一下改键的步骤。

<!-- more -->

### 准备

安装 Mac 下改键神器 [Karabiner-Elements](https://pqrs.org/osx/karabiner/) ，目前已支持最新系统 Catalina。

```bash
brew cask install karabiner-elements
```

安装过程需要输入用户密码。安装完成后先打开该软件，根据提示把所需权限加上，再退出，此时用户目录下会出现相应的配置文件夹，下一步增加配置文件需要用到。

### 增加配置文件

进入配置文件夹下，增加配置文件。

```bash
cd ~/.config/karabiner/assets/complex_modifications
vim custom-capslock.json
```

添加配置：

```js
{
    "title": "Change caps_lock to Esc and Control",
    "rules": [
        {
            "description": "Post Esc if Caps is tapped, Control if held.",
            "manipulators": [
                {
                    "type": "basic",
                    "from": {
                        "key_code": "caps_lock",
                        "modifiers": {
                            "optional": [
                                "any"
                            ]
                        }
                    },
                    "to": [
                        {
                            "key_code": "left_control",
                            "lazy": true
                        }
                    ],
                    "to_if_alone": [
                        {
                            "key_code": "escape"
                        }
                    ]
                }
            ]
        }
    ]
}
```

### 软件设置

打开 karabiner-elements，如图进行设置。

![Xnip2019-10-14_17-47-20](https://tva1.sinaimg.cn/large/006y8mN6gy1g7xw6mma96j31cs0u00zy.jpg)

![Xnip2019-10-14_17-52-56](https://tva1.sinaimg.cn/large/006y8mN6gy1g7xw758t7nj31gk0osjwe.jpg)

### 参考链接

- [参考配置步骤](https://medium.com/@pechyonkin/how-to-map-capslock-to-control-and-escape-on-mac-60523a64022b)
- [参考配置文件](https://pqrs.org/osx/karabiner/json.html#typical-complex_modifications-examples-post-escape-if-left-control-is-pressed-alone)
