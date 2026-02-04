# AI 换衣应用实现计划

## 产品概述

一个个人试衣应用，用户上传照片后可从预设衣服库中选择服装，AI 生成换衣效果，并保存历史记录。

## 核心功能

| 功能 | 说明 | 价值 |
|------|------|------|
| 首页 | 应用介绍、快速开始入口 | 降低使用门槛 |
| AI试衣 | 上传照片 + 选择衣服 → 生成效果 | 核心价值 |
| 衣服库 | 按分类浏览预设衣服 | 丰富选择 |
| 历史记录 | 查看/重新编辑过去的换衣记录 | 用户留存 |

## 用户流程

```
首页 → 上传照片 → 选择衣服 → AI处理 → 查看结果 → 保存
```

## 设计系统

**风格**: 时尚现代，优雅紫粉渐变
- 主色: `hsl(280, 70%, 50%)` - 时尚紫
- 强调色: `hsl(350, 80%, 65%)` - 珊瑚粉
- 背景: 米白色系

## 文件结构

### 需要创建的文件

```
src/
├── pages/
│   ├── TryOn.tsx           # 试衣主页面
│   ├── Wardrobe.tsx        # 衣服库页面
│   └── History.tsx         # 历史记录页面
├── components/
│   ├── layout/
│   │   └── Header.tsx      # 导航头部
│   ├── try-on/
│   │   ├── ImageUploader.tsx
│   │   ├── ClothingSelector.tsx
│   │   ├── ClothingCard.tsx
│   │   ├── TryOnResult.tsx
│   │   └── ProcessingOverlay.tsx
│   ├── wardrobe/
│   │   └── WardrobeGrid.tsx
│   ├── history/
│   │   ├── HistoryList.tsx
│   │   └── HistoryCard.tsx
│   └── home/
│       ├── HeroSection.tsx
│       └── FeatureCards.tsx
├── stores/
│   ├── tryOnStore.ts       # 试衣状态
│   └── historyStore.ts     # 历史记录 (localStorage持久化)
├── types/
│   └── index.ts            # 类型定义
├── data/
│   └── presetClothes.ts    # 预设衣服数据
└── services/
    └── tryOnService.ts     # AI换衣服务 (模拟)
```

### 需要修改的文件

| 文件 | 修改内容 |
|------|----------|
| `src/index.css` | 添加完整设计系统 CSS 变量 |
| `src/App.tsx` | 添加路由: `/try-on`, `/wardrobe`, `/history` |
| `src/pages/Index.tsx` | 重构为首页 |

## 技术方案

### AI 换衣
- 先使用模拟服务（显示处理动画 + 返回示例图）
- 后续可集成真实 AI API (如 Replicate fashn/tryon)

### 历史记录存储
- 使用 Zustand + localStorage 本地持久化
- 保留最近 50 条记录

### 预设衣服库
- 静态数据文件，包含 20-30 件预设服装
- 分类: 上衣、下装、连衣裙、外套

## 实施顺序

1. **设计系统** - 配置 index.css 变量
2. **布局组件** - Header 导航
3. **首页** - Hero + 功能介绍
4. **衣服库** - 预设数据 + 展示网格
5. **试衣页面** - 上传 + 选择 + AI 处理 + 结果展示
6. **历史记录** - 存储 + 展示 + 管理

## 验证方式

1. 访问首页，检查导航和 Hero 区域
2. 进入试衣页面，上传图片并选择衣服
3. 触发 AI 处理，查看加载动画和结果
4. 检查历史记录是否正确保存
5. 刷新页面，验证历史记录持久化
6. 移动端响应式测试
