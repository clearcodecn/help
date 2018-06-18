### mac 必备软件一览

* [sublime Text](https://www.sublimetext.com/)
    * 主题 afterFlow 
    * [配置](./sublime.md)
    * 插件
    ... 

* [iterm2](https://www.iterm2.com/)
* [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

```
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

* [chrome](https://www.google.cn/intl/zh-CN/chrome/?brand=CHBD&gclid=EAIaIQobChMIs_v-yMzd2wIVRSUrCh0ZXA51EAAYASAAEgJ2efD_BwE&gclsrc=aw.ds&dclid=CNjukczM3dsCFUh6vQodpKYGPg#)
* [搜狗输入法](https://pinyin.sogou.com/mac/)

* [homebrew](https://brew.sh/)
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
    * [替换brew源为国内源](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)
    ```
        cd "$(brew --repo)"
        git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git

        cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
        git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git

        brew update
    ```

* [shadowsocks](https://github.com/shadowsocks/shadowsocks)
    * [mac客户端](https://github.com/shadowsocks/shadowsocks-iOS/releases) [点击下载](https://github.com/shadowsocks/shadowsocks-iOS/releases/download/2.6.3/ShadowsocksX-2.6.3.dmg)
* [sourcetree](https://www.sourcetreeapp.com/)  [下载](https://downloads.atlassian.com/software/sourcetree/Sourcetree_2.7.6a.zip?_ga=2.48486435.485353572.1529338562-933830212.1529338562)











