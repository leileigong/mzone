# QSS样式

Qt样式表\(Qt Style Sheets\)是一种强大的机制.允许您定制widgets的外观,除了已经通过继承于QStyle之外。概念、术语和语法的Qt样式表大量的灵感来自HTML层叠样式表\(CSS\)，但适应的是小部件。样式表可以设置文本规范,在整个应用程序使用QApplication::setStyleSheet\(\)或在一个特定的窗口小部件\(和子部件\)使用QWidget::setStyleSheet\(\)。如果有几个样式表设置在不同层次上,Qt的有效样式表来自于这些所有的设置。这就是所谓的级联。

## 属性

## border-style 

border-style 属性用于设置元素所有边框的样式，或者单独地为各边设置边框样式。只有当这个值不是 none 时边框才可能出现。

| 值 | 描述 |
| :--- | :--- |
| none | 定义无边框。 |
| hidden | 与 "none" 相同。不过应用于表时除外，对于表，hidden 用于解决边框冲突。 |
| dotted | 定义点状边框。在大多数浏览器中呈现为实线。 |
| dashed | 定义虚线。在大多数浏览器中呈现为实线。 |
| solid | 定义实线。 |
| double | 定义双线。双线的宽度等于 border-width 的值。 |
| groove | 定义 3D 凹槽边框。其效果取决于 border-color 的值。 |
| ridge | 定义 3D 垄状边框。其效果取决于 border-color 的值。 |
| inset | 定义 3D inset 边框。其效果取决于 border-color 的值。 |
| outset | 定义 3D outset 边框。其效果取决于 border-color 的值。 |
| inherit | 规定应该从父元素继承边框样式。 |

* 上边框是点状
* 右边框是实线
* 下边框是双线
* 左边框是虚线

```
border-style:dotted solid double dashed;
```



* 上边框是点状
* 右边框和左边框是实线
* 下边框是双线

```css
border-style:dotted solid double;
```



* 上边框和下边框是点状
* 右边框和左边框是实线

```css
border-style:dotted solid;
```



* 所有 4 个边框都是点状

```css
border-style:dotted;
```

###  border-color

```css
border-color: rgb(255, 0, 127);
```

## 示例

#### 设置下划线样式的输入框

* 背景透明且无边框 （下划线使用绘图事件画条线）

方法1：

```css
background:transparent;border-width:0;border-style:outset
```

```cpp
lineEdit->setStyleSheet("background:transparent;border-width:0;border-style:outset");
```

方法2：

```css
background:transparent;border-width:1;border-style:none none solid none;
```

![](../.gitbook/assets/image%20%284%29.png)



