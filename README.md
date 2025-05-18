# VarTypes

Robocup 的 grSim 仿真需要的包，十分古老，已经不再维护了。正在修复中，试兼容现代项目，方便跨系统编译。

内容引用自 [github上不知名同好](https://github.com/szi/vartypes")。


# 修复内容

- QT4 改为 QT6
- CMakeLists.txt 适配现代编译器和 QT6
- `<trl/memory>` 头文件改为 `<memory>`
- std::trl 改为 std
- setMargin(1); 改为 setContentsMargins(1, 1, 1, 1);

# 编译方法

```bash
mkdir build && cd build
cmake ..
make
# 安装
make install # 会安装到项目内部
```

