# QSS样式

Qt样式表\(Qt Style Sheets\)是一种强大的机制.允许您定制widgets的外观,除了已经通过继承于QStyle之外。概念、术语和语法的Qt样式表大量的灵感来自HTML层叠样式表\(CSS\)，但适应的是小部件。样式表可以设置文本规范,在整个应用程序使用QApplication::setStyleSheet\(\)或在一个特定的窗口小部件\(和子部件\)使用QWidget::setStyleSheet\(\)。如果有几个样式表设置在不同层次上,Qt的有效样式表来自于这些所有的设置。这就是所谓的级联。

