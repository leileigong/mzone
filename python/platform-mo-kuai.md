---
description: 通过模块级的API函数提供获取底层平台信息的接口
---

# platform模块



```text
# 支持的平台
    
Still needed:
#    * support for MS-DOS (PythonDX ?)
#    * support for Amiga and other still unsupported platforms running Python
#    * support for additional Linux distributions
```



* architecture

获取`python`系统架构位宽（32位还是64位）,非操作系统架构的位宽

```python
platform.architecture() 
('32bit', 'ELF') # python 2.7.13 32bits on 树莓派3B+
('32bit', 'ELF') # python 3.5.3 32bits on 树莓派3B+
('64bit','ELF') # python 3.6. 64 bits on debian jessie 64 bits
('32bit','WindowsPE') # python 2.7.10 32 bits on windows 8/10 64 bits 
('32bit','WindowsPE') # python 3.6.6 32 bits on windows 8/10 64 bits 
('64bit','WindowsPE') # python 3.6.6 64 bits on wndows 8/10 64 bits 
('64bit', '') # python 3.4.1 64 bits on mac os x 10.9.4
```

{% hint style="info" %}
ELF和WindowsPE是可执行文件格式
{% endhint %}

* system

操作系统 linux,mac还是windows

```python
platform.system() 
'Linux'     # python 2.7.13 32bits on 树莓派3B+
'Linux'     # python 3.5.3 32bits on 树莓派3B+
'Linux'     # python 3.6. 64 bits on debian jessie 64 bits
'Windows'     # python 2.7.10 32 bits on windows 8/10 64 bits 
'Windows'     # python 3.6.6 32 bits on windows 8/10 64 bits 
'Windows'     # python 3.6.6 64 bits on wndows 8/10 64 bits 
'Darwin'      # python 3.4.1 64 bits on mac os x 10.9.4
```



* version  系统版本

```python
platform.version() 
'#1122 SMP Tue Jun 19 12:26:26 BST 2018'     # python 2.7.13 32bits on 树莓派3B+
'#1122 SMP Tue Jun 19 12:26:26 BST 2018'    # python 3.5.3 32bits on 树莓派3B+
'#1 SMP Debian 3.10.11-1 (2013-09-10)'     # python 3.6. 64 bits on debian jessie 64 bits
'6.2.9200'     # python 2.7.10 32 bits on windows 8/10 64 bits 
'10.0.17134'   # python 3.6.6 32 bits on windows 8/10 64 bits 
'10.0.17134'   # python 3.6.6 64 bits on wndows 8/10 64 bits 
'Darwin Kernel Version 13.3.0: Tue Jun  3 21:27:35 PDT 2014; root:xnu-2422.110.17~1/RELEASE_X86_64'      # python 3.4.1 64 bits on mac os x 10.9.4
```

* machine  \(CPU平台\)

```python
platform.machine() 
'armv7l'     # python 2.7.13 32bits on 树莓派3B+
'Linux'     # python 3.5.3 32bits on 树莓派3B+
'x86_64'     # python 3.6. 64 bits on debian jessie 64 bits
'AMD64'     # python 2.7.10 32 bits on windows 8/10 64 bits 
'AMD64'     # python 3.6.6 32 bits on windows 8/10 64 bits 
'AMD64'     # python 3.6.6 64 bits on wndows 8/10 64 bits 
'x86_64'      # python 3.4.1 64 bits on mac os x 10.9.4
```

* dist \(linux发行版\) 

{% hint style="danger" %}
```
Python 3.5之后该API已废弃
```
{% endhint %}

```python
platform.dist()
('debian', '9.4', '')     # python 2.7.13 32bits on 树莓派3B+
('debian', '9.4', '')     # python 3.5.3 32bits on 树莓派3B+
('debian','jessie/sid', '')  # python 3.6. 64 bits on debian jessie 64 bits
('', '', '')     # python 2.7.10 32 bits on windows 8/10 64 bits 
('', '', '')     # python 3.6.6 32 bits on windows 8/10 64 bits 
('', '', '')     # python 3.6.6 64 bits on wndows 8/10 64 bits 
('', '', '')      # python 3.4.1 64 bits on mac os x 10.9.4
```



* node \(节点名/机器名\)

```python
platform.node() 
'raspberrypi'（默认）     # python 2.7.13 32bits on 树莓派3B+
'raspberrypi'（默认）     # python 3.5.3 32bits on 树莓派3B+
'xxx'     # python 3.6. 64 bits on debian jessie 64 bits
'xxx'     # python 2.7.10 32 bits on windows 8/10 64 bits 
'xxx'     # python 3.6.6 32 bits on windows 8/10 64 bits 
'xxx'     # python 3.6.6 64 bits on wndows 8/10 64 bits 
'xxx'      # python 3.4.1 64 bits on mac os x 10.9.4
```

* uname \(系统信息\)



```python
platform.uname() 
# 元组     # python 2.7.13 32bits on 树莓派3B+
('Linux', 'raspberrypi', '4.14.50-v7+', '#1122 SMP Tue Jun 19 12:26:26 BST 2018', 'armv7l', '')     

#platform.uname_result实例     # python 3.5.3 32bits on 树莓派3B+
uname_result(system='Linux', node='raspberrypi', release='4.14.50-v7+', version='#1122 SMP Tue Jun 19 12:26:26 BST 2018', machine='armv7l', processor='')     

# python 3.6. 64 bits on debian jessie 64 bits
uname_result(system='Linux', node='work', release='3.10-3-amd64', version='#1 SMP Debian 3.10.11-1 (2013-09-10)', machine='x86_64', processor='') 

# python 2.7.10 32 bits on windows 8/10 64 bits 
('Windows',
 'DESKTOP-AM65SOJ',
 '8',
 '6.2.9200',
 'AMD64',
 'Intel64 Family 6 Model 142 Stepping 9, GenuineIntel')

# python 3.6.6 32 bits on windows 8/10 64 bits 
uname_result(system='Windows', node='DESKTOP-AM65SOJ', release='10', version='10.0.17134', machine='AMD64', processor='Intel64 Family 6 Model 142 Stepping 9, GenuineIntel')

# python 3.6.6 64 bits on wndows 8/10 64 bits 
uname_result(system='Windows', node='DESKTOP-AM65SOJ', release='10', version='10.0.17134', machine='AMD64', processor='Intel64 Family 6 Model 142 Stepping 9, GenuineIntel')

# python 3.4.1 64 bits on mac os x 10.9.4
uname_result(system='Darwin', node='mba', release='13.3.0', version='Darwin Kernel Version 13.3.0: Tue Jun  3 21:27:35 PDT 2014; root:xnu-2422.110.17~1/RELEASE_X86_64', machine='x86_64', processor='i386')

```



* python\_version （python版本）

```python
platform.python_version() 
'2.7.13'   # python 2.7.13 32bits on 树莓派3B+
'3.5.3'    # python 3.5.3 32bits on 树莓派3B+
'3.6.6'     # python 3.6.6 64 bits on debian jessie 64 bits
'2.7.10'     # python 2.7.10 32 bits on windows 8/10 64 bits 
'3.6.6'     # python 3.6.6 32 bits on windows 8/10 64 bits 
'3.6.6'     # python 3.6.6 64 bits on wndows 8/10 64 bits 
'3.4.1'      # python 3.4.1 64 bits on mac os x 10.9.4
```



* sys.platform  

```python
sys.platform
'linux2'   # python 2.7.13 32bits on 树莓派3B+
'linux2'    # python 3.5.3 32bits on 树莓派3B+
            # python 3.6.6 64 bits on debian jessie 64 bits
'win32'     # python 2.7.10 32 bits on windows 8/10 64 bits 
'win32'     # python 3.6.6 32 bits on windows 8/10 64 bits 
'win32'     # python 3.6.6 64 bits on wndows 8/10 64 bits 
'darwin'      # python 3.4.1 64 bits on mac os x 10.9.4
```

