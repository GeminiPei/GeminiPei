# Django创建方法

## 1、创建

```django
django-admin startproject 项目名称
```

## 2、运行项目

```django
python3 manage.py runserver
```

## 3、创建组件

```django
python3 manage.py startapp 组件名称
```

## 4、设置数据库配置

根目录修改文件  /setting.py  文件

```python
DATABASE = {
	'default': {
    # python自带的一个数据库，基本不会被使用
    # 'ENGINE': 'jango.db.backends.sqlite3',   ——本地储存，常用于APP等需要将数据储存到用户本地时
    # 'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    # 默认: BASE_DIR / 'db.sqlite3'
    # 注册我们自己使用的数据库链接
    'ENGINE': 'django.db.backends.mysql', # 数据库引擎
    'NAME': 'databasename', # 数据库名称
    'USER': 'root', # 连接数据库的用户名称
    'PASSWORD': 'databasepassword', # 用户密码
    'HOST': '127.0.0.1', # 访问的数据库的主机ip地址
    'PORT': '3306', # 默认mysql访问端口
  }
}
```

## 5、数据引入 更新数据库mysql

```python
python3 manage.py migrate
```

## 6、新建 功能

```python
python3 manage.py startapp 功能名称
```

## 7、功能配置  models.py

```python
from django.db import models
class 功能名称(models.Model):
  功能属性名称 = models.CharField(max_length=200) //200字节
```

### 附：Django model数据（字段）类型

|               字段名                | 释义                                                         |
| :---------------------------------: | :----------------------------------------------------------- |
|              AutoField              | 一个自动递增的整型字段，添加记录时它会自动增长。你通常不需要直接使用这个字段；如果你不指定主键的话，系统会自动添加一个主键字段到你的model |
|            BooleanField             | 布尔字段，管理工具里会自动将其描述为checkbox                 |
|              CharField              | 字符串字段，单行输入，用于较短的字符串（如要保存大量文本，使用TextField）CharField有一个必填参数： |
|        CharField.max_length:        | 字符的最大长度，django会根据这个参数在数据库层和校验层限制该字段所允许的最大字符数 |
|              TextField              | 一个容量很大的文本字段，例：admin管理界面用多行编辑框表示该字段数据 |
|     CommaSeparatedIntegerField      | 用于存放逗号分隔的整数值。类似CharField，必须maxlength参数   |
|              DateField              | 日期字段，有下列额外的可选参数                               |
|              auto_now:              | 当对象被保存时，自动将该字段的值设置为当前时间，通常用于表示“last-modified”时间戳； |
|            auto_now_add:            | 当对象首次被创建时，自动将该字段的值设置为当前时间，通常用于表示对象创建时间 |
|            DateTimeField            | 类似DateField，支持同样的附加选项                            |
|             EmailField              | 一个带有检查Email合法性的CharField，不接受maxlength参数      |
|              FileField              | 一个文件上传字段，要求一个必须有的参数：                     |
|             upload_to,              | 一个用于保存上载文件的本地文件系统路径，这个路径必须包含strftime formatting，该格式将被上载文件的date/time替换 |
| 使用FileField或ImageField需要此步骤 | 在setting文件中，定义一个完整路径给MEDIA_ROOT，以便让Django在此处保存上传文件。（出于性能考虑，这些文件并不保存到数据库）；定义MEDIA_URL作为该目录的公共URL |
|            FilePathField            | 选择指定目录，按限制规则选择文件，有三个参数可选，其中“path”是必需的 |
|               path：                | 必需参数，一个目录的绝对文件系统路径                         |
|               match：               | 可选参数，一个正则表达式，作为一个字符串，FilePathField将使用它过滤文件名，注意这个正则表达式只会应用到base filename而不是路径全名 |
|             recursive：             | 可选参数，是否包括path下全部子目录，True或False，默认是False |
|             FloatField              | 浮点型字段                                                   |
|            max_digits：             | 总位数（不包括小数点和符号）                                 |
|          decimal_places：           | 小数位数                                                     |
|             ImageField              | 类似FileField，不过要校验上传对象是否是一个合法图片，它有两个可选参数： |
|     height_field：width_field：     | 图片将提供的高度和宽度规格保存，该字段要求python imaging库   |
|            IntegerField             | 用于保存一个整数                                             |
|           IPAddressField            | 一个字符串的IP地址                                           |
|          NullBooleanField           | 类似BooleanField，不过允许NULL作为其中一个选项，推荐使用该字段而非BooleanField+null=True选项 |
|          PhoneNumberField           | 一个带有合法美国风格电话号码校验的CharField（格式：XXX-XXX-XXXX） |
|        PositiveIntegerField         | 类似IntegerField，但取值范围为非负整数                       |
|     PositiveSmallIntergerField      | 正小整型字段，类似PositiveIntegerField，取值范围较小（数据库相关） |
|              SlugField              | “slug”是一个报纸术语，是某个东西的小小标记（短签），只包含字母、数字、下划线和连字符，它们通常用于URLs |
|            max_length：             | 可指定值，若未指定，默认长度：50                             |
|         prepopulate_from：          | 来源于slug的自动预置列表                                     |
|          SmallIntegerField          | 类似于IntegerField，不过只允许某个取值范围内的整数（依赖数据库） |
|              TimeField              | 时间字段，类似于DateField和DateTimeField                     |
|              URLField               | 用于保存URL，“verify_exists=True（默认）”，给定的URL会预先检查是否存在（即URL是否被有效装入且没有返回404响应） |
|            USStateField             | 美国州名缩写，由两个字母组成                                 |
|              XMLField               | XML字符字段，校验值是否为合法XML的TextField，必须提供参数：  |
|            schema_path：            | 校验文本的RelaxNG schema的文件系统路径                       |
|                附：                 | Field选项                                                    |
|                选项                 | 释义                                                         |
|                null                 | 缺省设置为false，通常不将其用于字符型字段上，如CharField，TextField，字符型字段如果没有值会返回空字符串 |
|                blank                | 该字段是否可以为空，若false则必须有值                        |
|               choice                | 用来选择值的二维元组，第一个是实际存储的值，第二个用来方便进行选择 |
|                core                 | db_column，db_index = True，该字段创建索引                   |
|               default               | 设置缺省值                                                   |
|              editable               | 若为false，admin模式下将不能改写，缺省为真                   |
|              help_text              | admin模式下帮助文档                                          |
|             primary_key             | 设置主键，如果没有设置django创建表时会自动加上：id = meta.AutoField('ID',primary_key=True) |
|                                     | primary_key=True暗示着blank=False，null=False和unique=True   |
|             radio_admin             | 用于admin模式下将select转换为radio显示，只用于ForeignKey或者设置了choices |
|               unique                | 数据唯一                                                     |
|           unique_dor_date           | 日期唯一，如下例中系统将不允许title和pub_date两个都相同的数据重复出现title=meta.CharField(maxlength=30,unique_for_date='pub_date') |
|           validator_list            | 有效性检查，非有效产生django.core.validators.validationError错误 |

### 图片类型模块生成方法

```python
img_URL = models.ImageField(upload_to="上传地址", verbose_name="图片")
img_URL = models.ImageField(upload_to='一级目录/', verbose_name="图片地址")
```

在跨域设置中设置上传设置方法，请见“Django实现跨域.md”

## 8、功能引入项目

在  /根目录/setting.py  添加

```python
INSTALLED_APPS = [
  功能名称.apps.功能名称Config,
]
```

## 9、功能数据写入mysql

```python
python3 manage.py makemigrations 功能名称
```

## 10、创建超级管理员

```python
python3 manage.py createsuperuser
```

## 11、使用超级管理员登陆后台

## 12、功能引入后台管理  admin.py

```python
from django.contrib import admin
from .models import 功能名称
class 功能名称Admin(admin.ModelAdmin):
  list_display = ["名称"]
admin.site.register(功能名称, 功能名称Admin)
```

## 13、安装 django-rest-framework

```python
pip3 install djangorestframework
pip3 install markdown  # Markdown support for the browsable API
pip3 install django-filter  # Filtering support
```

## 14、配置drf  settings.py

```python
INSTALLED_APPS = [
  ...
  'rest_framework',
]
```

```python
REST_FRAMEWORK = {
  'DEFAULT_PERMISSION_CLASSES': [
    'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly'，  #忽略权限问题可直接访问
    'rest_framework.permissions.IsAdminUser',  #浏览器只有登陆的时候才能访问，否则会报权限错误
  ]
}
```

### 组件目录 新建  serializers.py  序列化文件

```python
from rest_framework import serializers
from .models import 组件名称
class 组件名称Serializer(serializers.ModelSerializer):
  class Meta:
    model = 组件名称
    fields = ["组件模块名称"]
```

### 组件目录 修改  views.py  页面显示

```python
from django.shortcuts import render
from .serializers import 组件名称Serializer
from .models import 组件名称
# Create your views here.
from rest_framework import viewsets, mixins

class 组件名称Views(viewsets.modelViewSet):
  serializer_class = 组件名称Serializer
  def get_queryset(self):
    return 组件名称.objects.all()
```

## 15、根目录  urls.py  配置API路由

```python
from django.contrib import admin
from django.urls import path, include
from rest_framework import routers
router = routers.DefaultRouter()  #自动路由
from 组件名称.views import 组件名称Views
router.register('组件名称',组件名称Views,basename='组件名称')

urlpatterns = [
  path('admin/', admin.site.urls),
  path('', include(router.urls)),
  path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```

## 16、根目录  urls.py  图片引入设置

```python
from django.views.static import serve  # 服务
from 项目名称.settings import MEDIA_ROOT  # 访问方法
# 一般上述方法即可实现，如还是显示不出，添加下列语句并在urlpatterns中加上最下方语句
from 项目名称 import settings
from django.conf.urls.static import static

urlpatterns = [
  url('一级目录/path.*', serve, {"document_root": MEDIA_ROOT}),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)  # 如果访问不到图片可加上句语句尝试
```

## 17、Django 文件模型

### models.py 中

```python
class 项目名称(models.Model):
  img = midels.ImageField(upload_to="video_img")  # 视频缩略图
  video = models.FileField(upload_to="video")  # 视频
```
