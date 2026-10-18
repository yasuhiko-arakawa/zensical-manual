---
icon: lucide/palette
---

# シンタックスハイライトの確認

C++、CMake、console(ターミナル)の配色を確認するためのページです。
配色は `stylesheets/extra.css` で定義しています。

## C++

```cpp
#include <iostream>
#define MAX 10

// コメント
namespace app {

class Foo : public Base {
public:
  int add(const std::string& s, int n) { return n + 1; }
};

}  // namespace app

int main() {
  auto x = 3.14;
  std::cout << "hello\n" << MAX << x;
  if (x > 0) return 0;
}
```

## CMake

```cmake
cmake_minimum_required(VERSION 3.20)
project(demo LANGUAGES CXX)

# コメント
set(CMAKE_CXX_STANDARD 17)
add_executable(demo main.cpp)
target_link_libraries(demo PRIVATE ${LIB_NAME})

if(WIN32)
  message(STATUS "windows")
endif()
```

## ターミナル(console)

` ```console ` のブロックは、Ubuntu の bash を VSCode のターミナルで見たときの配色になります。
入力したコマンドは色分けせず、プロンプトを緑にします。

### 基本

```console
$ uv run zensical build
Build started
No issues found
```

### Ubuntu のプロンプト

```console
ubuntu@host:~/proj$ ls -la # コメント
total 8
drwxr-xr-x 2 ubuntu ubuntu 4096 Oct 19 10:00 build
ubuntu@host:~/proj$ echo "hello $HOME" && git status
hello /home/ubuntu
$ cat missing.txt
cat: missing.txt: No such file or directory
```
