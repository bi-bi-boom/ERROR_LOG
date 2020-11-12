---
title: 基于 Python 的 Kivy 开发：首次配置 kivy
date: 2020-11-08 00:32:30
categories:
- Kivy
tags:
- "author: zanxinz"
- Python
---

## kivy

- kivy 是一个基于 Python 的 App 开发框架，基于 kivy进行移动端的 APP 开发是一个不错的选择。
- 首先，演示一下在 win10 环境下配置 kivy。

1.直接 `pip install kivy`

- 自己写个 main.py 作为测试

```py
from kivy.app import App
from kivy.uix.label import Label

class MainApp(App):
    def build(self):
        label = Label(text='Hello from Kivy',
                      size_hint=(.5, .5),
                      pos_hint={'center_x': .5, 'center_y': .5})

        return label

if __name__ == '__main__':
    app = MainApp()
    app.run()
```

<!-- More -->

- 如果遇到问题
  
```html
[CRITICAL] [App         ] Unable to get a Text provider, abort.
```

则 terminal 执行下列语句（可能需要梯子）

```shell
pip install --upgraade pip wheel setuptools
pip install docutils pygments pypiwin32 kivy.deps.sdl2 kivy.deps.glew
pip install kivy.deps.gstreamer
pip install kivy.deps.angle
pip install --upgrade kivy
```

2.运行之后可以看见下图，说明成功

{% asset_img kivySuccess.png %}
