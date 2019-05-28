# beetl安装

### 创建spring boot工程

Group: com.template

Artifact: beetl-demo

使用如下Maven坐标：

```markup
<dependency>
    <groupId>com.ibeetl</groupId>
    <artifactId>beetl</artifactId>
    <version>2.9.6</version>
</dependency>
```

![](../.gitbook/assets/image%20%283%29.png)

### 默认配置文件

默认配置文件在jar包中。beetl-2.9.6.jar\org\beetl\core\beetl-default.properties



```typescript
#######默认配置
ENGINE=org.beetl.core.engine.DefaultTemplateEngine #引擎实现类
DELIMITER_PLACEHOLDER_START=${    #占位符号
DELIMITER_PLACEHOLDER_END=}
DELIMITER_STATEMENT_START=<%      #语句的定界符号
DELIMITER_STATEMENT_END=%>
DIRECT_BYTE_OUTPUT = FALSE    # IO输出模式，默认是FALSE,即通常的字符输出
# 指定了支持HTML标签，且符号为#,默认配置下，模板引擎识别<#tag ></#tag>这样的类似html标签，并能调用相应的标签函数或者模板文件。
# 你也可以指定别的符号，如bg: 则识别<bg:
HTML_TAG_SUPPORT = true
HTML_TAG_FLAG = #
# 如果标签属性有var，则认为是需要绑定变量给模板的标签函数
HTML_TAG_BINDING_ATTRIBUTE = var
# 指定允许本地Class直接调用
NATIVE_CALL = TRUE
TEMPLATE_CHARSET = UTF-8    # 指定模板字符集是UTF-8
# 指定异常的解析类，默认是ConsoleErrorHandler，他将在render发生异常的时候在后台打印出错误信息（System.out)。
ERROR_HANDLER = org.beetl.core.ConsoleErrorHandler
# 指定了本地Class调用的安全策略
NATIVE_SECUARTY_MANAGER= org.beetl.core.DefaultNativeSecurityManager
# 配置了是否进行严格MVC，通常情况下，此处设置为false.
MVC_STRICT = FALSE

### 资源配置，resource后的属性只限于特定ResourceLoader ###
### 指定了默认使用的模板资源加载器，注意，在beetl与其他MVC框架集成的时候，模板加载器不一定根据这个配置，
### 比如spring，他的RESOURCE_LOADER以spring的配置为准
RESOURCE_LOADER=org.beetl.core.resource.ClasspathResourceLoader
#classpath 跟路径，与框架集成的时候，此配置会被框架代码覆盖而不能生效
RESOURCE.root= /
#是否检测文件变化
RESOURCE.autoCheck = TRUE
### 配置了自定义的方法所在的目录以及文件名后缀。
### beetl既支持通过java类定义方法，也支持通过模板文件来定义方法
#自定义脚本方法文件位置
RESOURCE.functionRoot = functions
#自定义脚本方法文件的后缀
RESOURCE.functionSuffix = html

### 配置了自定义的html标签所在的目录以及文件名后缀。
### beetl既支持通过java类定义标签，也支持通过模板文件来定义标签
#自定义标签文件位置
RESOURCE.tagRoot = htmltag
#自定义标签文件后缀
RESOURCE.tagSuffix = tag

#如果采用beetl集成的web应用，可以在渲染模板前调用如下类,此类必须实现WebRenderExt接口
WEBAPP_EXT = 

#允许html function or Tag 使用特殊的定界符，因为function或者tag通常有大量beetl语句
FUNCTION_TAG_LIMITER=

#####  扩展，也可以通过特定框架注册##############
## 内置的方法
# 注册了一个date方法，其实现类是org.beetl.ext.fn.DateFunction
FN.date = org.beetl.ext.fn.DateFunction
FN.nvl = org.beetl.ext.fn.NVLFunction
FN.debug = org.beetl.ext.fn.DebugFunction
#兼容以前版本，用has代替
FN.exist = org.beetl.ext.fn.CheckExistFunction
FN.has = org.beetl.ext.fn.CheckExistFunction
FN.printf = org.beetl.ext.fn.Printf
FN.decode = org.beetl.ext.fn.DecodeFunction
FN.assert = org.beetl.ext.fn.AssertFunction
FN.print = org.beetl.ext.fn.Print
FN.println = org.beetl.ext.fn.Println
FN.printFile = org.beetl.ext.fn.PrintFile
FN.trunc = org.beetl.ext.fn.TruncFunction
FN.trim = org.beetl.ext.fn.TruncFunction2
#兼容以前版本 empty，用isEmpty代替
FN.empty = org.beetl.ext.fn.EmptyFunction
FN.qmark = org.beetl.ext.fn.QuestionMark
FN.isEmpty = org.beetl.ext.fn.EmptyExpressionFunction
FN.isNotEmpty = org.beetl.ext.fn.IsNotEmptyExpressionFunction
FN.parseInt = org.beetl.ext.fn.ParseInt
FN.parseLong = org.beetl.ext.fn.ParseLong
FN.parseDouble= org.beetl.ext.fn.ParseDouble
FN.range = org.beetl.ext.fn.Range
FN.flush = org.beetl.ext.fn.Flush
FN.json = org.beetl.ext.fn.Json
FN.pageCtx = org.beetl.ext.fn.PageContextFunction
FN.type.new=org.beetl.ext.fn.TypeNewFunction
FN.type.name=org.beetl.ext.fn.TypeNameFunction
FN.global=org.beetl.ext.fn.DynamicGlobalValueFunction
FN.hasAttribute=org.beetl.ext.fn.HasAttributeFunction



##内置的功能包
# 注册了一个方法包strutil，其实现类org.beetl.ext.fn.StringUtil，此类的每个public方法都将注册为beetl的方法
FNP.strutil = org.beetl.ext.fn.StringUtil
FNP.reg = org.beetl.ext.fn.RegxFunctionUtil

FNP.array = org.beetl.ext.fn.ArrayUtil

##内置的格式化函数
# 注册了一个日期格式化函数
FT.dateFormat =  org.beetl.ext.format.DateFormat
FT.numberFormat =  org.beetl.ext.format.NumberFormat
##内置的默认格式化函数
FTC.java.util.Date = org.beetl.ext.format.DateFormat
FTC.java.sql.Date = org.beetl.ext.format.DateFormat
FTC.java.sql.Time = org.beetl.ext.format.DateFormat
FTC.java.sql.Timestamp = org.beetl.ext.format.DateFormat
FTC.java.lang.Short = org.beetl.ext.format.NumberFormat
FTC.java.lang.Long = org.beetl.ext.format.NumberFormat
FTC.java.lang.Integer = org.beetl.ext.format.NumberFormat
FTC.java.lang.Float = org.beetl.ext.format.NumberFormat
FTC.java.lang.Double = org.beetl.ext.format.NumberFormat
FTC.java.math.BigInteger = org.beetl.ext.format.NumberFormat
FTC.java.math.BigDecimal = org.beetl.ext.format.NumberFormat
FTC.java.util.concurrent.atomic.AtomicLong = org.beetl.ext.format.NumberFormat
FTC.java.util.concurrent.atomic.AtomicInteger = org.beetl.ext.format.NumberFormat

##虚拟属性 无
## 标签类
TAG.include= org.beetl.ext.tag.IncludeTag
TAG.includeFileTemplate= org.beetl.ext.tag.IncludeTag
TAG.layout= org.beetl.ext.tag.LayoutTag
TAG.delete= org.beetl.ext.tag.DeleteTag
TAG.htmltag= org.beetl.ext.tag.HTMLTagSupportWrapper2
TAG.htmltagvar= org.beetl.ext.tag.HTMLTagVarBindingWrapper
TAG.cache= org.beetl.ext.tag.cache.CacheTag

# 输出优化，设定字符串转字符输出buffer最大长度，每个线程默认是4K，buffer存放在SoftRefercen里，否则是Weak,通过enableThreadLocal 禁用这个特性
# 注意，这是一个全局设置，会导致每个GroupTemplate都是一样的，因为他只跟线程相关，跟GroupTemplate无关，其他配置是跟GroupTemplate有关
GLOBAL.buffer.maxSize=4096
GLOBAL.enableThreadLocal=true
GLOBAL.buffer.isInSoft=true
```





### GroupTemplate基本用法

#### **字符串模板加载器**

在创建GroupTemplate过程中，如果传入的是StringTemplateResourceLoader，则允许通过调用gt.getTemplate\(String template\)来获取模板实例对象，如下所示

```java
    public static void demo1GroupTemplate() throws IOException {
        //new一个模板资源加载器
        StringTemplateResourceLoader resourceLoader = new StringTemplateResourceLoader();
        /* 使用Beetl默认的配置。
         * Beetl可以使用配置文件的方式去配置，但由于此处是直接上手的例子，
         * 我们不去管配置的问题，只需要基本的默认配置就可以了。
         */
        Configuration cfg = Configuration.defaultConfiguration();

        //step1. Beetl的核心GroupTemplate
        GroupTemplate gt = new GroupTemplate(resourceLoader, cfg);

        //step2. 需要通过GroupTemplate将自己定义的String模板加载为Beetl模板——Template
        Template t = gt.getTemplate("title:${title}\nhello,${name}");

        //step3. 使用template中的操作，将数据和占位符绑定
        //将变量titlename传入模板里
        t.binding("title","This is a test template Email.");
        //将变量name传入模板里
        t.binding("name", "beetl");

        //step4. 渲染模板，得到输出
        String str = t.render();
        System.out.println(str);
    }
```

#### **文件资源模板加载器**

更通常情况下，模板资源是以文件形式管理的，集中放在某一个文件目录下（如webapp的模板根目录就可能是WEB-INF/template里），因此，可以使用FileResourceLoader来加载模板实例，如下代码：



```java
public static void demo2FileGroupTemplate() throws IOException{
    String root = System.getProperty("user.dir")+ File.separator+"template";
    FileResourceLoader resourceLoader = new FileResourceLoader(root,"utf-8");
    Configuration cfg = Configuration.defaultConfiguration();
    GroupTemplate gt = new GroupTemplate(resourceLoader, cfg);
    Template t = gt.getTemplate("/s01/hello.txt");
    String str = t.render();
    System.out.println(str);
}
```

#### **Classpath资源模板加载器**

还有种常情况下，模板资源是打包到jar文件或者同Class放在一起，因此，可以使用ClasspathResourceLoader来加载模板实例，如下代码：

```java
public static void demo3ClassGroupTemplate() throws IOException{
    ClasspathResourceLoader resourceLoader = new ClasspathResourceLoader("org/beetl/sample/s01/");
    Configuration cfg = Configuration.defaultConfiguration();
    GroupTemplate gt = new GroupTemplate(resourceLoader, cfg);
    Template t = gt.getTemplate("/hello.txt");
    String str = t.render();
    System.out.println(str);
}
```







