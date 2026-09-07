# The-third-experiment-of-Fundamentals-of-system-development-tools


## 第 9 题 从源码构建并在干净环境安装 Wheel

**主题**：Packaging and Shipping Code
**建议用时**：12—15 分钟

在 q09 中按给定内容创建一个最小 Python 命令行包，并验证 wheel 安装。

给定内容

```
# src/greetlab/cli.py
import argparse

def main():
    p = argparse.ArgumentParser()
    p.add_argument("--name", required=True)
    a = p.parse_args()
    print(f"Hello, {a.name}!")
```

```
# pyproject.toml
[build-system]
requires = ["setuptools>=68"]
build-backend = "setuptools.build_meta"

[project]
name = "greetlab-学号"
version = "0.1.0"

[project.scripts]
sdt-greet = "greetlab.cli:main"
```

题目要求

- 创建`src/greetlab/__init__.py`、给定的`cli.py` 和`pyproject.toml`，并把 “学号” 替换为自己的学号。
- 在已安装 build 工具的课程环境中运行 `python -m build`，生成 wheel。
- 新建一个干净虚拟环境，只从生成的 wheel 安装。
- 切换到 q09 之外运行 `sdt-greet --name <学号>`，确认输出正确。

## 第 10 题 让编程智能体进入可验证的修复循环

**主题**：智能体编程
**建议用时**：12—15 分钟

复用第 9 题的 greetlab 包，使用编程智能体完成一个小型测试驱动修复。

题目要求

- 复制 q09 为 q10，添加一个失败测试：当 name 只含空白字符时，main 应以`SystemExit(2)`结束。
- 先运行测试确认失败，再向编程智能体说明目标、约束和测试命令，要求它修改实现并运行测试。
- 人工检查 diff，撤销无关修改，并再次运行测试。
- 在`ai_log.md` 中用不超过 5 行记录核心提示、智能体改动和人工验证。

## 第 11 题 把 “无法处理” 的协作材料改成可执行信息

**主题**：不止于代码
**建议用时**：12—15 分钟

围绕 “空姓名仍输出问候语” 这一缺陷，改写下面三段质量较差的协作材料。

给定内容

> 
> Issue:Windows 上运行不了，尽快修复。
> 提交信息:fix bug
> 评审意见：这里写得不好，重写。

已知事实：运行`sdt-greet --name " "` 时仍输出`Hello, !`，并以 0 退出。

题目要求

- 在`communication.md` 中重写 Issue，包含环境、复现命令、期望结果和实际结果；未知信息写 “待确认”。
- 重写提交信息：标题使用祈使语气，正文说明问题和解决方案。
- 重写评审意见：指出具体行为、风险和建议动作，并标注`Blocking`、`Suggestion` 或`Nit`。
- 全文控制在 400 字以内，保持专业、简洁。

## 第 12 题 修复一个可复现的线性回归训练循环

**主题**：Python 与 PyTorch
**建议用时**：12—15 分钟

将下方代码保存为`q12/train.py`，补全 TODO 并完成一次 PyTorch CPU 训练。

给定内容

```
import torch
from torch import nn

torch.manual_seed(20260907)
x = torch.linspace(-1, 1, 101).reshape(-1, 1)
y = 3 * x - 1

loss_fn = nn.MSELoss()
model = nn.Linear(1, 1)
opt = torch.optim.SGD(model.parameters(), lr=0.1)

for _ in range(200):
    # TODO:进入评估模式并在no_grad 中打印最终损失、weight 和bias
    pred = model(x)
    loss = loss_fn(pred, y)
    # TODO:清空梯度、反向传播、更新参数
```

题目要求

- 补全训练循环，正确调用`zero_grad`、`backward` 和`step`。
- 训练后调用`model.eval()`，并在`torch.no_grad()`中计算最终损失。
- 打印最终损失、weight 和 bias；最终损失应小于 0.001。
- 不得直接把 weight 和 bias 赋值为 3 和−1。

 如何在干净环境中安装Wheel？

 除了Python和PyTorch，还有哪些常用的系统开发工具？

 智能体编程的应用场景有哪些？
