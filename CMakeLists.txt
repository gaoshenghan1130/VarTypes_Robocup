cmake_minimum_required(VERSION 3.16)

project(vartypes)

set(CMAKE_PREFIX_PATH "/Users/gaoshenghan/Qt/6.9.0/macos")

# 找 Qt6 的 Widgets 模块
find_package(Qt6 COMPONENTS Widgets REQUIRED)
# 用现代 CMake 风格查找 Boost
find_package(Boost 1.88 REQUIRED COMPONENTS serialization)




# 开启自动 moc、rcc、uic
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

set(src_dir .)

include_directories(
  ${src_dir}/vartypes
  ${src_dir}/vartypes/primitives
  ${src_dir}/vartypes/enhanced
  ${src_dir}/vartypes/gui
  ${src_dir}/vartypes/xml
)

set(SRCS
  ${src_dir}/vartypes/VarBase64.cpp
  ${src_dir}/vartypes/VarNotifier.cpp
  ${src_dir}/vartypes/VarTypes.cpp
  ${src_dir}/vartypes/VarXML.cpp
  ${src_dir}/vartypes/VarTypesInstance.cpp
  ${src_dir}/vartypes/VarTypesFactory.cpp
  ${src_dir}/vartypes/xml/xmlParser.cpp

  ${src_dir}/vartypes/primitives/VarStringVal.cpp
  ${src_dir}/vartypes/primitives/VarBoolVal.cpp
  ${src_dir}/vartypes/primitives/VarVal.cpp
  ${src_dir}/vartypes/primitives/VarIntVal.cpp
  ${src_dir}/vartypes/primitives/VarDoubleVal.cpp
  
  ${src_dir}/vartypes/primitives/VarType.cpp
  ${src_dir}/vartypes/primitives/VarBlob.cpp
  ${src_dir}/vartypes/primitives/VarBool.cpp
  ${src_dir}/vartypes/primitives/VarDouble.cpp
  ${src_dir}/vartypes/primitives/VarExternal.cpp
  ${src_dir}/vartypes/primitives/VarInt.cpp
  ${src_dir}/vartypes/primitives/VarList.cpp
  ${src_dir}/vartypes/primitives/VarQWidget.cpp
  ${src_dir}/vartypes/primitives/VarSelection.cpp
  ${src_dir}/vartypes/primitives/VarString.cpp
  ${src_dir}/vartypes/primitives/VarStringEnum.cpp
  ${src_dir}/vartypes/primitives/VarTrigger.cpp

  ${src_dir}/vartypes/gui/VarItem.cpp
  ${src_dir}/vartypes/gui/VarItemDelegate.cpp
  ${src_dir}/vartypes/gui/VarTreeModel.cpp
  ${src_dir}/vartypes/gui/VarTreeView.cpp
  ${src_dir}/vartypes/gui/VarTreeViewOptions.cpp

  ${src_dir}/vartypes/primitives/VarProtoBufferVal.cpp
  ${src_dir}/vartypes/primitives/VarProtoBuffer.cpp

  ${src_dir}/vartypes/primitives/VarAnyVal.cpp
  ${src_dir}/vartypes/primitives/VarAny.cpp
)

set(RC
  ${src_dir}/vartypes/gui/icons/icons.qrc
)

# 不用 qt4_wrap_cpp，开启 CMAKE_AUTOMOC 会自动处理所有需要 moc 的头文件

# Debug/Release 编译选项
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-DNDEBUG -O3 -march=native")

# Qt6 库
set(libs Qt6::Widgets)

# 安装到项目目录下的 install 文件夹
set(CMAKE_INSTALL_PREFIX "${CMAKE_SOURCE_DIR}/install")
set(CMAKE_INSTALL_INCLUDEDIR "include")
set(CMAKE_INSTALL_LIBDIR "lib")
set(CMAKE_INSTALL_DOCDIR "doc")

# 生成动态库
add_library(vartypes SHARED ${SRCS} ${RC})
set_target_properties(vartypes PROPERTIES VERSION 0.8.0 SOVERSION 1)

target_link_libraries(vartypes PRIVATE ${libs} Boost::serialization)
target_include_directories(vartypes PRIVATE ${Boost_INCLUDE_DIRS})
message(STATUS "Boost include dir: ${Boost_INCLUDE_DIRS}")
message(STATUS "Boost libraries: ${Boost_LIBRARIES}")


# 安装规则
install(FILES
  ${src_dir}/vartypes/primitives/VarType.h
  ${src_dir}/vartypes/primitives/VarBlob.h
  ${src_dir}/vartypes/primitives/VarBool.h
  ${src_dir}/vartypes/primitives/VarDouble.h
  ${src_dir}/vartypes/primitives/VarExternal.h
  ${src_dir}/vartypes/primitives/VarInt.h
  ${src_dir}/vartypes/primitives/VarList.h
  ${src_dir}/vartypes/primitives/VarQWidget.h
  ${src_dir}/vartypes/primitives/VarSelection.h
  ${src_dir}/vartypes/primitives/VarString.h
  ${src_dir}/vartypes/primitives/VarStringEnum.h
  ${src_dir}/vartypes/primitives/VarTrigger.h
  ${src_dir}/vartypes/gui/VarItem.h
  ${src_dir}/vartypes/gui/VarItemDelegate.h
  ${src_dir}/vartypes/gui/VarTreeModel.h
  ${src_dir}/vartypes/gui/VarTreeView.h
  ${src_dir}/vartypes/VarNotifier.h
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/vartypes)

install(FILES
  ${src_dir}/README.md
  ${src_dir}/COPYING
  DESTINATION ${CMAKE_INSTALL_DOCDIR}/vartypes
)

install(TARGETS vartypes
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

message(STATUS "Include dir: ${CMAKE_INSTALL_INCLUDEDIR}")
message(STATUS "Install prefix: ${CMAKE_INSTALL_PREFIX}")
