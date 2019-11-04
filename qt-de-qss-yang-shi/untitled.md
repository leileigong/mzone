# QLabel设置图片

#### 图片自适应QLabel大小

```python
class Example (QWidget):
    def __init__(self):
        super ().__init__ ()
        self.initUI ()
        def initUI(self):
            hbox = QHBoxLayout (self)
            lbl = QLabel (self)
            pixmap = QPixmap ("E:\programming\python\MineSweeper\mine.jpg")  # 按指定路径找到图片，注意路径必须用双引号包围，不能用单引号
            lbl.setPixmap (pixmap)  # 在label上显示图片
            lbl.setScaledContents (True)  # 让图片自适应label大小
            hbox.addWidget (lbl)
            self.setLayout (hbox)
            self.move (300, 200)
            self.setWindowTitle ('Red Rock')
            self.show ()
```

#### 移除label上得图片

```python
lbl.setPixmap(QPixmap(""))#移除label上的图片
```

