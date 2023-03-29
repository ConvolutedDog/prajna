# 般若编程语言

般若是一门专门为构建更加模块化, 自动化和智能化的人工智能基础设施而研发的编程语言. 般若编程语言的目标是同时满足人工智能研究, 训练和部署等多个阶段的使用; 可以简易使用的CPU, GPU和各种NPU为人工智能提供算力.

```mermaid
graph LR
    CPU --> Prajna
    GPU --> Prajna
    NPU --> Prajna

    Prajna --> Training
    Prajna --> Deployment
    Prajna --> Research
```

## 特点

### 即时编译

般若采用即时编译方式, 代码即程序, 无需事先编译为二进制可执行程序. 可以直接在X86, Arm和RiscV等各种指令集的芯片上直接运行. 采用LLVM作为后端, 所以会有着和C/C++一样的性能.

### 异构编程

般若将同时提供对CPU, GPU和NPU的编程支持. 目前般若不止提供类似于CUDA的核函数编写, 还提供了gpu for等简单高效的并行编程范式, 会极大低降低异构/并行编程的复杂性. 后期会加大对各种芯片的支持力度

### 张量计算

般若后面会集成类型于MLIR和TVM的张量优化技术, 提供高效, 并行乃至分布式计算的支持. 把张量计算相关的并行计算, 分布式计算的支持放在底层, 会非常有利于后续神经网络等框架的开发.

### 语法改善

般若是属于类C语言, 借鉴Rust了的面向对象的设计(Swift), 移除不必要的语法特性, 例如引用等. 内存管理采用比较通用的引用计数.

### 友好交互

般若支持main函数, Repl和Jupyter等多种交互方式, 适合算法研发和部署等多种场景.

## 代码示例

```
import ::gpu;

func main(){
    var shape = [10, 20];
    var tensor0 = Tensor<i64, 2>::create(shape);
    var tensor1 = Tensor<i64, 2>::create(shape);
    var tensor2 = Tensor<i64, 2>::create(shape);

    for idx in [0, 0] to shape {
        tensor0.at(idx) = 1;
        tensor1.at(idx) = 2;
    }

    @gpu // 标注后, 会自动拷贝数据到gpu上
    for idx in [0, 0] to shape{
        tensor2.at(idx) = tensor0.at(idx) + tensor1.at(idx);
    }

    // 运行完后, gpu的数据会自动拷贝的主机上
    for idx in [0, 0] to shape{
        debug::assert(tensor2.at(idx) == 3);
    }
}
```

## 文档

可以查阅[般若编程语言指南](docs/般若编程语言指南.md)来进一步了解.

## 架构

下图是一个般若相关的思维导图, 显示了般若项目的一些规划和构成.

```mermaid
mindmap
  root((Prajna))
    Backend
      LLVM
      Wasmtime
    Paramita Runtime
        Tensor Computing Optimization
          Polyhedral Optimization
          TVM
          MLIR
        Auto Diff
        Symbol Compute
    Framework
      Nerual Networks
      Mathmatics Tools
    IDE
      Vscode
        ISP
        Debug
      Jupyter
        PyWidgets
        Notebook


```

下面是般若编译器相关的的路线图

```mermaid
timeline
    title 玄青矩阵路线图
    般若编程语言: 编译器实现: 数据可视化: IDE
    波罗蜜多运行时: 张量计算优化: 自动微分: 符号计算
    框架: 数学库: 神经网络库: AutoML
    应用: 视觉/语音/NPL: 自动驾驶: 多模态大模型

```

## 合作

项目本身还有很多问题, 需要组建一个团队才能克服, 故在此寻求天使投资, 期望更多志同道合的朋友加入.

有任何建议和问题都可以添加微信"zhangzhimin-tju"联系我.

如果有芯片, 自动驾驶, 科学计算等领域的朋友感兴趣, 欢迎一起探讨下如何展开合作.

招聘实习生, 本科及其以上学历, 最好一周能投入16个小时以上. 1. 具备一定的编程和数学基础 2. 对编译器和人工智能基础设施很有兴趣. 不必担心没有项目经验和相关基础, 很容易学的. 可以加微信直接投递简历.
