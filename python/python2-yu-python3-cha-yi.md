---
description: 字符与编码
---

# python2与python3差异

#### python2内置的字符串类包含basestring/str/bytes/unicode/

str和bytes意义相同都表示二进制字符串；

bytes-----decode\('utf8'\)解码---&gt; unicode

str-----decode\('utf8'\)解码---&gt; unicode

* basestring基类

```python
In [2]: help(basestring)
Help on class basestring in module __builtin__:

class basestring(object)
 |  Type basestring cannot be instantiated; it is the base for str and unicode.
 |
 |  Data and other attributes defined here:
 |
 |  __new__ = <built-in method __new__ of type object>
 |      T.__new__(S, ...) -> a new object with type S, a subtype of T
```

* basestring派生bytes

```python
In [3]: help(bytes)
Help on class str in module __builtin__:

class str(basestring)
 |  str(object='') -> string
 |
 |  Return a nice string representation of the object.
 |  If the argument is a string, the return value is the same object.
 |
 |  Method resolution order:
 |      str
 |      basestring
 |      object
```

* basestring派生str

```python
In [7]: help(str)
Help on class str in module __builtin__:

class str(basestring)
 |  str(object='') -> string
 |
 |  Return a nice string representation of the object.
 |  If the argument is a string, the return value is the same object.
 |
 |  Method resolution order:
 |      str
 |      basestring
 |      object
```

* basestring派生unicode

```python
In [8]: help(unicode)
Help on class unicode in module __builtin__:

class unicode(basestring)
 |  unicode(object='') -> unicode object
 |  unicode(string[, encoding[, errors]]) -> unicode object
 |
 |  Create a new Unicode object from the given encoded string.
 |  encoding defaults to the current default string encoding.
 |  errors can be 'strict', 'replace' or 'ignore' and defaults to 'strict'.
 |
 |  Method resolution order:
 |      unicode
 |      basestring
 |      object
```

#### python2内置的字符串类包含str/bytes

删除了内置basestring和内置类unicode，str和bytes都是直接继承object.

str表示Unicode字符串，bytes表示二进制字符串

* str类

```python
In [12]: help(str)
Help on class str in module builtins:

class str(object)
 |  str(object='') -> str
 |  str(bytes_or_buffer[, encoding[, errors]]) -> str
 |
 |  Create a new string object from the given object. If encoding or
 |  errors is specified, then the object must expose a data buffer
 |  that will be decoded using the given encoding and error handler.
 |  Otherwise, returns the result of object.__str__() (if defined)
 |  or repr(object).
 |  encoding defaults to sys.getdefaultencoding().
 |  errors defaults to 'strict'.
```

* bytes类

```python
In [11]: help(bytes)
Help on class bytes in module builtins:

class bytes(object)
 |  bytes(iterable_of_ints) -> bytes
 |  bytes(string, encoding[, errors]) -> bytes
 |  bytes(bytes_or_buffer) -> immutable copy of bytes_or_buffer
 |  bytes(int) -> bytes object of size given by the parameter initialized with null bytes
 |  bytes() -> empty bytes object
 |
 |  Construct an immutable array of bytes from:
 |    - an iterable yielding integers in range(256)
 |    - a text string encoded using the specified encoding
 |    - any object implementing the buffer API.
 |    - an integer
```



#### 示例代码变量

```python
#python2:
string_unicode_u        = u"\x11\x22\x33\xAA\xBB\CC\x30\x31\x32"
string_binary_default   =  "\x11\x22\x33\xAA\xBB\CC\x30\x31\x32"
string_binary           = b"\x11\x22\x33\xAA\xBB\CC\x30\x31\x32"

#python3:
string_unicode_u        = u"\x11\x22\x33\xAA\xBB\CC\x30\x31\x32"
string_unicode_default  = "\x11\x22\x33\xAA\xBB\CC\x30\x31\x32"
string_binary           = b"\x11\x22\x33\xAA\xBB\CC\x30\x31\x32"

```

* join用法示例

```python
# python3:
In [50]: help(str.join)
Help on method_descriptor:

join(...)
    S.join(iterable) -> str

    Return a string which is the concatenation of the strings in the
    iterable.  The separator between elements is S.
    
# 错误用法1：bytes字符串直接用作join参数
''.join(string_binary)
# TypeError: sequence item 0: expected str instance, int found 

 b''.join(string_binary) 
# TypeError: sequence item 0: expected a bytes-like object, int found

# 错误用法2：unicode字符串join bytes字符串
b''.join(string_unicode_u)
TypeError: sequence item 0: expected a bytes-like object, str found
        
```



* 用法示例

```python
In [20]: binascii.b2a_hex(string_binary)
Out[20]: b'112233aabb5c4343303132'

In [21]: binascii.b2a_hex(string_unicode_u)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-21-5acba6d47c67> in <module>
----> 1 binascii.b2a_hex(string_unicode_u)

TypeError: a bytes-like object is required, not 'str'

In [22]: binascii.b2a_hex(string_unicode_u.encode('utf8'))
Out[22]: b'112233c2aac2bb5c4343303132'

In [23]:
```

```python
#python2 
In [4]: string_binary_default == string_binary
Out[4]: True
In [5]: id(string_binary)
Out[5]: 68588864
In [6]: id(string_binary_default)
Out[6]: 68588992

#python3 
In [4]: string_unicode_u == string_unicode_default
Out[4]: True
In [5]: string_unicode_u == string_binary
Out[5]: False
In [6]: id(string_unicode_u)
Out[6]: 2604114192936
In [7]: id(string_unicode_default)
Out[7]: 2604116763552
```

#### 列表推导式对字符串的处理差异

输入字符串分为两种：

1. unicode字符串
2.  二进制字符串

* 在python2中列表推导式从输入unicode字符串中取得字符不做转换
* 在python2中列表推导式从输入二进制字符串中取得字符不做转换
* 在python3中列表推导式从输入unicode字符串中取得字符不做转换
* 在python3中列表推导式从输入二进制字符串中取得字符转换成整数

```python
#python2
In [7]: [c for c in string_unicode_u]
Out[7]: [u'\x11', u'"', u'3', u'\xaa', u'\xbb', u'\\', u'C', u'C', u'0', u'1', u'2']

In [9]: [c for c in string_binary]
Out[9]: ['\x11', '"', '3', '\xaa', '\xbb', '\\', 'C', 'C', '0', '1', '2']

#python3
In [8]: [c for c in string_unicode_u]
Out[8]: ['\x11', '"', '3', 'ª', '»', '\\', 'C', 'C', '0', '1', '2']

In [9]: [c for c in string_binary]
Out[9]: [17, 34, 51, 170, 187, 92, 67, 67, 48, 49, 50]
```

#### list对字符串的处理差异**（同列表推导式）**

```python
#python2
In [33]: list(string_unicode_u)
Out[33]: [u'\x11', u'"', u'3', u'\xaa', u'\xbb', u'\\', u'C', u'C', u'0', u'1', u'2']

In [34]: list(string_binary)
Out[34]: ['\x11', '"', '3', '\xaa', '\xbb', '\\', 'C', 'C', '0', '1', '2']


#python3
In [52]: list(string_unicode_u)
Out[52]: ['\x11', '"', '3', 'ª', '»', '\\', 'C', 'C', '0', '1', '2']

In [53]: list(string_binary)
Out[53]: [17, 34, 51, 170, 187, 92, 67, 67, 48, 49, 50]
```



