# 軍事化魔法少女創作協作專案

## 專案目的

這是一個多 agent 協作的創作專案。透過 Claude Code 派發任務給不同的 subagent，模擬一個編劇室 + 跑團 的混合工作流程，補完一個既有架構但仍有大量空窗的故事。

## 工作流程概述

主對話 agent 扮演 **GM（統籌者）** 的角色，根據場景需要：

1. **編劇統籌模式**：當情節已有明確走向時，GM 推進劇情、控制節奏與份量
2. **跑團模式**：當需要補完空窗時，GM 召喚角色 agent，讓她們在場景中互動，產出素材

所有角色 agent **必須能聽到同場景中其他角色的發言**，並保有對該場景的記憶。記憶透過檔案系統持久化。

## 目錄結構

```
magical_girl_project/
├── README.md（本檔案）
│
├── 世界觀核心/              ← 所有 agent 必讀
│   ├── world_bible.md       世界觀聖經
│   ├── narrative_priority.md 情節份量分配清單
│   └── story_skeleton.md    故事骨架與當前進度
│
├── 角色/                    ← 角色的「人設檔」，較穩定
│   ├── hana.md
│   ├── israfil.md
│   └── japanese_mg_lead.md
│
├── 角色狀態/                ← 角色的「當前狀態」，隨進度更新
│   ├── hana_state.md
│   └── israfil_state.md
│
├── agent指令/               ← 給各類 agent 的指令文件
│   ├── GM.md                統籌 agent 指令
│   ├── character_agent_template.md
│   └── faction_agent_template.md
│
└── 產出/
    ├── scenes/              場景草稿（跑團原始記錄）
    ├── dialogues/           對話素材
    ├── worldbuilding_notes/ 世界觀補完筆記
    ├── 章節劇本/             最終產出 1：對話劇本（少量動作提示）
    └── 章節大綱/             最終產出 2：故事大綱
```

## 兩種最終產出

1. **章節劇本**：逐章節編排，以對話為主，動作提示精簡
2. **章節大綱**：逐章節編排，敘事性的故事概要

## 使用方式

詳見 `agent指令/GM.md`。簡言之：
- 開始一個工作階段時，告訴 GM 你想推進哪一部分（章節編號 + 模式）
- GM 會自動讀取必要的檔案、召喚角色 agent、整合產出
- 每個階段結束時，GM 會更新「角色狀態」與「故事骨架」檔案
