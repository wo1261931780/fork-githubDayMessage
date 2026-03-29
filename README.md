# 🌤️ fork-githubDayMessage - 微信天气推送

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![License](https://img.shields.io/badge/License-Unknown-lightgrey)

## 📖 项目简介

fork-githubDayMessage是微信天气推送工具,通过微信公众平台API发送每日天气、纪念日、励志语录等模板消息到微信客户端。

## 📦 项目来源

- **原项目**: 未知(待确认)
- **原作者**: 未知
- **开源协议**: 未明确标注(需查看原项目)
- **Fork时间**: 2024年

## 🔧 二次开发内容

本项目为原项目的学习研究版本,主要用于:
- 学习微信公众平台API的使用
- 研究定时任务和消息推送技术
- 了解第三方API的集成方法

## ⚠️ 免责声明

本项目仅供学习研究使用,请勿用于商业用途或非法用途。使用本项目所产生的一切后果由使用者自行承担。

## 系统架构 | System Architecture

```mermaid
graph TB
    subgraph Input["📥 数据源"]
        A[天气API] --> B[城市定位]
        C[纪念日计算] --> D[恋爱天数]
        E[生日信息] --> F[生日提醒]
        G[每日一言API] --> H[励志语录]
    end
    
    subgraph Process["⚙️ 数据处理"]
        B --> I[天气数据组装]
        D --> I
        F --> I
        H --> I
        I --> J[模板变量填充]
        J --> K[微信模板消息]
    end
    
    subgraph Output["📤 推送服务"]
        K --> L[微信公众平台API]
        L --> M[模板消息发送]
        M --> N[微信客户端]
    end
    
    subgraph Schedule["⏰ 定时任务"]
        O[Cron定时器] --> P[每日触发]
        P --> A
        P --> G
    end
    
    style A fill:#e1f5ff
    style C fill:#e1f5ff
    style E fill:#e1f5ff
    style N fill:#c8e6c9
    style O fill:#fff9c4
```

## 消息推送流程 | Message Flow

```mermaid
sequenceDiagram
    participant S as 定时调度器
    participant W as 天气API
    participant Q as 一言API
    participant P as 数据处理器
    participant M as 微信API
    participant U as 用户微信
    
    S->>S: 每日定时触发
    S->>W: 请求城市天气
    W->>S: 返回天气数据
    
    S->>Q: 请求每日一言
    Q->>S: 返回励志语录
    
    S->>P: 组装消息数据
    Note over P: 计算恋爱天数<br/>检查生日提醒<br/>填充模板变量
    
    P->>M: 调用模板消息API
    M->>U: 推送微信消息
    
    U->>U: 显示推送内容
    Note over U: 城市、天气、温度<br/>恋爱天数、生日提醒<br/>励志语录
```

## 模板变量说明 | Template Variables

```mermaid
mindmap
  root((消息模板))
    基础信息
      日期
      城市
    天气数据
      天气状况
      气温
      风向
    纪念日
      恋爱天数
      生日1
      生日2
    每日一言
      英文语录
      中文翻译

## 📊 系统架构

```mermaid
flowchart TB
    subgraph Scheduler["⏰ 定时调度"]
        Cron["定时任务<br/>每日触发"]
    end
    
    subgraph DataFetcher["📡 数据获取"]
        Weather["天气API<br/>获取天气数据"]
        Love["恋爱天数<br/>计算天数"]
        Birthday["生日提醒<br/>生日倒计时"]
    end
    
    subgraph Template["📝 模板引擎"]
        Engine["模板渲染"]
        Data["数据填充"]
    end
    
    subgraph WeChat["💬 微信推送"]
        API["微信模板消息API"]
        User["用户接收"]
    end
    
    Cron --> DataFetcher
    DataFetcher --> Template
    Template --> WeChat
    
    Weather --> Engine
    Love --> Engine
    Birthday --> Engine
    Engine --> Data
    Data --> API
    API --> User
    
    classDef schedulerStyle fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef fetchStyle fill:#e3f2fd,stroke:#1565c0,stroke-width:2px
    classDef templateStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef wechatStyle fill:#e8f5e9,stroke:#388e3c,stroke-width:2px
    
    class Cron schedulerStyle
    class Weather,Love,Birthday fetchStyle
    class Engine,Data templateStyle
    class API,User wechatStyle
```

## 🔄 推送流程

```mermaid
sequenceDiagram
    participant Timer as 定时器
    participant Fetcher as 数据获取
    participant Template as 模板引擎
    participant WeChat as 微信API
    participant User as 用户微信
    
    Timer->>Fetcher: 每日触发
    Fetcher->>Fetcher: 获取天气数据
    Fetcher->>Fetcher: 计算恋爱天数
    Fetcher->>Fetcher: 计算生日倒计时
    Fetcher->>Template: 传递数据
    Template->>Template: 渲染模板
    Template->>WeChat: 发送消息
    WeChat->>User: 推送到微信
```

{{date.DATA}} 

城市：{{region.DATA}} 

天气：{{weather.DATA}} 
气温：{{temp.DATA}} 
风向：{{wind_dir.DATA}} 
今天是我们恋爱的第{{love_day.DATA}}天 


{{birthday1.DATA}}

{{birthday2.DATA}}

{{note_en.DATA}} {{note_ch.DATA}}
