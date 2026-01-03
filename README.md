# RhyniX - 微观世界的寒武纪2.0探索者

**版本:** 1.0.0  
**许可证:** [GPL v3](./LICENSE)  
**目标平台:** ADLINK MXE-5500 (x86_64)  
**领域:** 仿生机器人, 微型机器人, 环境科学, 人工智能, 分布式系统

## 概述

RhyniX 是一个科研与工业级别的 C++/Python 算法平台，其设计灵感来源于寒武纪早期的微小节肢动物——瑞尼虫 (*Rhyniella praecursor*)。该项目旨在为模拟和实现瑞尼虫的生物特性（如微小体型、弹跳运动、环境适应性、腐食性分解能力）的微型机器人平台提供核心控制算法。

本库实现了包括环境习性评估、行为模式切换、腐食性物质处理、弹跳与爬行运动控制、刚体动力学、流体力学（微观尺度）以及材料力学（微型结构）在内的多个模块。

## 关键特性

*   **仿生智能:** 算法基于对瑞尼虫化石结构和行为模式的研究。
*   **工业级:** 为实时性能和可靠性而设计，适用于嵌入式系统如 ADLINK MXE-5500。
*   **高性能计算:** 支持 MPI 并行处理和 CUDA GPU 加速。
*   **GPL v3 许可:** 完全开源，允许学术和商业使用与修改。
*   **模块化设计:** 清晰的职责分离，便于维护和扩展。
*   **REST API:** 提供 FastAPI 接口，便于集成。
*   **数据库集成:** 使用 MySQL 存储状态和结果。

## 安装与部署 (ADLINK MXE-5500)

```bash
# 1. 克隆项目
git clone https://github.com/your-repo/rhynix.git # 替换为实际仓库 URL
cd rhynix

# 2. 安装依赖 (确保系统已安装 MPI, CUDA, MySQL 客户端)
sudo apt update
sudo apt install build-essential cmake libopenmpi-dev libopenmpi3 libeigen3-dev libmysqlclient-dev python3-dev python3-pip

# 3. 安装 Python 依赖
pip3 install -r requirements.txt

# 4. 构建 C++ 核心库
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release -DWITH_MPI=ON -DWITH_CUDA=ON ..
make -j$(nproc)

# 5. 安装库和 Python 绑定
sudo make install

# 6. 部署 API 服务 (示例)
# 确保 MySQL 服务已启动并配置好数据库
# python3 -m uvicorn api.main:app --host 0.0.0.0 --port 8000