# `Git` 主仓库嵌套子仓库相关知识点

### 应用场景及优势

- **主仓库 `niceAdmin` 嵌套子仓库 `nicevite` 前端UI框架**
- **主仓库文件不会包含全量子仓库文件**

### **首次创建主仓库** 拉取主仓库，添加子仓库

```
git clone git://github.com/username/project.git
cd project
git submodule add git://github.com/username/framework.git framework
git commit -m "added framework submodule"
```

### **一次性拉取主仓库及其所有子仓库**

```
git clone --recursive git://<repository-with-submodules>.git
```

### **拉取主仓库后，手动更新拉取子仓库**

> 注：先录取主仓库后，手动更新子仓库

```
git submodule update --init
```

或

```
# submodule 'framework' registered for path 'project'
git submodule init
# checkout submodule 'framework'
git submodule update
```

### **子仓库更新，同时主仓库记录子仓库版本**

```
cd project/framework
git pull
cd ..
git commit -m 'updated framework submodule'
```

### **子仓库配置**

> 修改根目录下 `.gitmodules` 文件，添加 `ignore = dirty` 子项

**`ignore` 子项说明**

```
untracked ：忽略 在子模块B(也就是projectB目录)新添加的，未受版本控制内容
dirty ： 忽略对projectB目录下受版本控制的内容进行了修改
all ： 同时忽略untracked和dirty
```