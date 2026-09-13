# zhsh

一个基于 AI-Native 理念开发的面向 Homelab 和个人服务器轻度运维领域开发的自然语言增强 Shell，适合对 Linux 和 command line language 具备一定了解的人在非生产、非敏感环境下使用。  

zhsh 目前安装包约为 `1.7M`，编译后本体仅约 `4M`，适合 Homelab 等受限环境下使用最基本的 LLM 增强能力。  

> 需要服务器本身支持连接网络，至少要保证与 LLM Provider 之间网络通畅


## 能力

zhsh 认为每句自然语言描述的任务可以在六个轮次，至多三次澄清中解决，这也是目前 zhsh 的能力基线。设定该基线本质是由于在其适用场景下，不宜提供诸如 Codex、Claude Code 或者
Open Claw、Workbuddy、Deepseek Harness 等长程任务能力。  

用户应当自行考虑问题解决方案或者观测系统的什么状态，并在上述限制内完成任务，也因此，zhsh 不保留任意任务轮次中的任意交互数据（除非开启了特定的 debug 模式，但也是用于排查 zhsh 本身的功能问题）。  

非自然语言的纯粹 command line language，如直接输入 `ls` 等，会直接交由内置的 `bash` 执行并输出。

支持使用 ollama 等，面向内网部署的大模型后端。  


## 限制

目前架构仍然是使用 `bash` 作为执行核心，但由于该架构下，一些 Job Control 无法实现，以及环境变量的传播方向限制，未实现较为复杂的 Builtin 实现，如 `export` 等。  

目前不保证 shell 脚本可以正常按照原始行为执行，不推荐使用 zhsh 执行脚本。

由于目前软件生态限制，如果某个服务器需要远程开发或者远程自动化，不要将 zhsh 设置为默认 shell。

## 请求格式及安全性设计
- [zhsh-safety](https://github.com/zhshell/zhsh-safety)：静默执行的安全规则
- [zhcodec-sdk](https://github.com/zhshell/zhcodec-sdk)：请求风格转换 SDK
  - [zhcodec-openai](https://github.com/zhshell/zhcodec-openai)：openai 风格的请求转换
  - [zhcodec-anthropic](https://github.com/zhshell/zhcodec-anthropic)：anthropic 风格的请求转换
