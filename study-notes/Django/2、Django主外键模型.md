# Django主外键模型

## 一对一关系

## models.py中添加

```python
class 组件名称(models.Model):
  数据名称 = models.字段选项(参数)

# 外键
class 组件名称Data(models.Model):
  主键ID = models.ForeignKey(主键名称, on_delete=models.CASCADE, related_name='项目名称_id')
  content = models.字段选项(参数)
```

### 功能数据引入 mysql

### 数据引入 更新数据库 mysql

### admin.py 中引入

```python
from .models import 项目名称Data

class 项目名称DataAdmin(admin.ModelAdmin):
  list_display = ['项目名称ID', 'content']
  
admin.site.register(项目名称Data, 项目名称DataAdmin)
```

### serializers.py 中引入

```python
from .models import 项目名称Data

class 项目名称DataSerializer(serializers.ModelSerializer):
  项目名称ID = 项目名称Serializer(many=True/False)  # 加上外键可调用主键的内容，False为显示，True为主键调用外键时显示使用
  
  class Meta:
    model = 项目名称Data
    fields = ['项目名称ID', 'content']
    
 # 主键调用外键
class 项目名称ShowDataSerializer(serializers.ModelSerializer):
  项目名称_id = 项目名称DataSerializer(many=True/False)  # True为显示，False为外键调用主键时显示使用
  class Meta:
    model = 主键名称
    fields = ['数据名称', '项目名称_id']
```

### views.py 中引入

```python
from .models import 项目名称Data
from .serializers import 项目名称DataSerializer

class 项目名称DataViews(viewsets.ModelViewSet):
  serializer_class = 项目名称DataSerializer
  
  def get_queryset(self):
    return 项目名称Data.objects.all()
  
# 主键调用外键内容显示页面
from 项目名称.serializers import 项目名称ShowDataSerializer

class 项目名称ShowDataViews(viewsets.ModelViewSet):
  serializer_class = 项目名称ShowDataSerializer
  
  def get_queryset(self):
    return 项目名称.objects.all()
```

### urls.py 中引入

```python
from 项目名称.views import 项目名称DataViews

router.register('项目名称data', 项目名称DataViews, basename='项目名称data')

# 主键调用外键内容显示页面
from 项目名称.views import 项目名称ShowDataViews

router.register('项目名称showdata', 项目名称ShowDataViews, basename='项目名称showdata')
```

### models.py 中加入

```python
class 内容下	
  def __str__(self)
  	return self.数据名称
```

