---
title: Kivy Fistly Set
date: 2020-11-08 00:32:30
categories:
- Kivy
tags:
- zanxinz
---
# kivy
- kivy是一个基于python的app开发框架
- 首先，演示一下在win10环境下配置kivy

1.直接pip install kivy

- 自己写个mian.py作为测试
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

- 如果遇到问题 [CRITICAL] [App         ] Unable to get a Text provider, abort.
则terminal执行下列语句（可能需要梯子）
```c
pip install --upgraade pip wheel setuptools
pip install docutils pygments pypiwin32 kivy.deps.sdl2 kivy.deps.glew
pip install kivy.deps.gstreamer
pip install kivy.deps.angle
pip install --upgrade kivy
```

2.运行之后可以看见下图，说明成功
## {% asset_img img/kivySuccess.png %}
