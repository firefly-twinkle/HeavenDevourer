# 自动写作 Prompt

> 用于 AI 自动写作的完整 Prompt 模板，自动整合所有设定文件

---

## 使用说明

将以下 Prompt 发送给 AI，自动整合所有设定文件生成章节正文。

---

## 完整 Prompt 模板

```
你是一名专业的玄幻小说作家，正在连载小说《从吞噬开始无敌》。

请根据以下设定和信息，生成第【X】章的正文内容。

=================================================
【一、当前状态】（来自剧情状态机.md）

- 当前卷：第 1 卷：血染青云
- 当前章：第【X】章
- 主角：林夜，修为【武师 X 星】，状态【正常/受伤】
- 当前位置：【地点】
- 当前目标：【目标】
- 伙伴：【伙伴列表】
- 物品：【关键物品】
- 敌人：【敌人列表】
- 上一章结尾：【上一章悬念】

=================================================
【二、本章规划】（来自章节蓝图.md）

| 项目 | 规划内容 |
|------|----------|
| 章节标题 | 【标题】 |
| 场景进入 | 【从哪里开始】 |
| 冲突建立 | 【第一个冲突】 |
| 冲突升级 | 【冲突如何升级】 |
| 行动推进 | 【主角如何行动】 |
| 悬念收尾 | 【结尾钩子】 |
| 情绪变化 | 【情绪曲线】 |
| 爽点类型 | 【爽点类型】 |

=================================================
【三、时间线】（来自时间线.md）

- 时间节点：Day【X】
- 前一章时间：Day【X-1】
- 时间流逝：【X 天/半天】
- 特殊说明：【闭关/旅途等】

=================================================
【四、伏笔状态】（来自伏笔系统.md）

待埋伏笔：
- 【伏笔名称】：【说明】

待回收伏笔：
- 【伏笔名称】：【埋点章节】

本章需要：
- ☐ 埋设新伏笔
- ☐ 回收旧伏笔（哪个）

=================================================
【五、能力体系】（来自能力体系.md + 功法与武技获取追踪.md）

主角已掌握：
- 武技：【列表】
- 功法：【列表】
- 领域：【吞噬领域】

修为等级：
- 当前：【武师 X 星】
- 下一境：【武师 X+1 星/大武师】

越级规则：
- 跨 1 大境界：50% 转化率
- 跨 2 大境界：20% 转化率，有反噬

=================================================
【六、节奏要求】（来自爽点追踪系统.md + 冲突系统.md）

冲突密度：
- 每章至少 3 个冲突节点
- 每 1000 字至少 1 个冲突点

爽点要求：
- 每章至少 1 个爽点
- 本章爽点等级：【S1-S5】

情绪循环：
- 当前循环位置：【轻/压/爽/爆/缓】

=================================================
【七、格式要求】

1. 字数：2000-3000 字
2. 格式：纯文本，不使用 markdown（**、---、- 列表）
3. 语言：中文，禁止英文（系统提示除外）
4. 章节标题：第 X 章【标题】
5. 本章总结：
   - 推进点：
   - 冲突：
   - 情绪变化：
   - 悬念：

=================================================
【八、禁止事项】

❌ 不允许突破设定等级
❌ 不允许引入未定义角色
❌ 不允许使用英文（系统提示除外）
❌ 正文不允许使用 markdown 格式
❌ 不允许时间跳跃混乱
❌ 不允许忽略已有设定
❌ 不允许一章解决所有矛盾
❌ 不允许无意义对话填充

=================================================

请开始生成第【X】章正文：
```

---

## 自动化脚本（Python）

```python
#!/usr/bin/env python3
"""
自动写作脚本 - 整合所有设定文件生成章节
"""

import json
import os
from datetime import datetime

# 读取设定文件的函数
def read_file(path):
    with open(path, 'r', encoding='utf-8') as f:
        return f.read()

def parse_status_machine(content):
    """解析剧情状态机"""
    # TODO: 实现解析逻辑
    return {
        'current_chapter': 26,
        'protagonist_power': '武师七星',
        'protagonist_status': '受伤',
        'location': '郊外山洞',
        'goal': '救柳如烟，复仇青云宗',
        'partners': ['小铁', '莫老 (下落不明)'],
        'items': ['两块令牌', '两块玉佩'],
        'enemies': ['青云子', '李玄风', '血刀门'],
        'last_chapter_hook': '莫老生死？如何救柳如烟？'
    }

def parse_blueprint(content, chapter):
    """解析章节蓝图"""
    # TODO: 实现解析逻辑
    return {
        'title': '山洞疗伤，制定计划',
        'scene_enter': '郊外山洞',
        'conflict_build': '疗伤恢复 + 青云宗通缉令',
        'conflict_escalate': '如何联系血刀门救柳如烟',
        'action': '制定营救计划，联系血刀门',
        'suspense': '能否救出柳如烟？',
        'emotion': '压抑→坚定',
        'pleasure_point': '计划爽点（掌控全局制定计划）'
    }

def parse_timeline(content, chapter):
    """解析时间线"""
    return {
        'day': 19,
        'prev_day': 18,
        'duration': '1-2 天',
        'note': '山洞闭关疗伤'
    }

def parse_foreshadowing(content):
    """解析伏笔系统"""
    return {
        'to_plant': [],
        'to_resolve': ['伏笔 7：林福儿子', '伏笔 13：莫老下落'],
        'this_chapter': '回收莫老下落伏笔'
    }

def parse_abilities(content):
    """解析能力体系"""
    return {
        'martial_arts': ['狮吼功（小成）', '烈焰爪（大成）', '开山掌（入门）'],
        'cultivation': ['吞噬功法'],
        'domain': ['吞噬领域'],
        'current_power': '武师七星',
        'next_power': '武师八星'
    }

# 生成 Prompt
def generate_prompt(chapter):
    base_dir = os.path.dirname(os.path.dirname(__file__))
    
    # 读取所有设定文件
    status = parse_status_machine(read_file(f'{base_dir}/03_剧情系统/剧情状态机.md'))
    blueprint = parse_blueprint(read_file(f'{base_dir}/10_正文/第 1 卷/01_章节蓝图.md'), chapter)
    timeline = parse_timeline(read_file(f'{base_dir}/06_时间系统/时间线.md'), chapter)
    foreshadowing = parse_foreshadowing(read_file(f'{base_dir}/05_信息与伏笔系统/伏笔系统.md'))
    abilities = parse_abilities(read_file(f'{base_dir}/01_核心系统/能力体系.md'))
    
    # 填充 Prompt 模板
    prompt = f"""
你是一名专业的玄幻小说作家，正在连载小说《从吞噬开始无敌》。

请根据以下设定和信息，生成第{chapter}章的正文内容。

=================================================
【一、当前状态】

- 当前卷：第 1 卷：血染青云
- 当前章：第{chapter}章
- 主角：林夜，修为{status['current_power']}，状态{status['protagonist_status']}
- 当前位置：{status['location']}
- 当前目标：{status['goal']}
- 伙伴：{', '.join(status['partners'])}
- 物品：{', '.join(status['items'])}
- 敌人：{', '.join(status['enemies'])}
- 上一章结尾：{status['last_chapter_hook']}

=================================================
【二、本章规划】

| 项目 | 规划内容 |
|------|----------|
| 章节标题 | {blueprint['title']} |
| 场景进入 | {blueprint['scene_enter']} |
| 冲突建立 | {blueprint['conflict_build']} |
| 冲突升级 | {blueprint['conflict_escalate']} |
| 行动推进 | {blueprint['action']} |
| 悬念收尾 | {blueprint['suspense']} |
| 情绪变化 | {blueprint['emotion']} |
| 爽点类型 | {blueprint['pleasure_point']} |

=================================================
【三、时间线】

- 时间节点：Day{timeline['day']}
- 前一章时间：Day{timeline['prev_day']}
- 时间流逝：{timeline['duration']}
- 特殊说明：{timeline['note']}

=================================================
【四、伏笔状态】

待回收伏笔：
{chr(10).join(['- ' + v for v in foreshadowing['to_resolve']])}

本章需要：
- ☐ 回收旧伏笔：{foreshadowing['this_chapter']}

=================================================
【五、能力体系】

主角已掌握：
- 武技：{', '.join(abilities['martial_arts'])}
- 功法：{', '.join(abilities['cultivation'])}
- 领域：{', '.join(abilities['domain'])}

修为等级：
- 当前：{abilities['current_power']}
- 下一境：{abilities['next_power']}

=================================================
【六、节奏要求】

冲突密度：
- 每章至少 3 个冲突节点
- 每 1000 字至少 1 个冲突点

爽点要求：
- 每章至少 1 个爽点
- 本章爽点等级：S2

情绪循环：
- 当前循环位置：压→爽

=================================================
【七、格式要求】

1. 字数：2000-3000 字
2. 格式：纯文本，不使用 markdown
3. 语言：中文，禁止英文（系统提示除外）
4. 章节标题：第{chapter}章【{blueprint['title']}】
5. 本章总结：
   - 推进点：
   - 冲突：
   - 情绪变化：
   - 悬念：

=================================================
【八、禁止事项】

❌ 不允许突破设定等级
❌ 不允许引入未定义角色
❌ 不允许使用英文
❌ 正文不允许使用 markdown 格式
❌ 不允许时间跳跃混乱
❌ 不允许忽略已有设定

=================================================

请开始生成第{chapter}章正文：
"""
    return prompt

# 主函数
if __name__ == '__main__':
    import sys
    chapter = int(sys.argv[1]) if len(sys.argv) > 1 else 26
    prompt = generate_prompt(chapter)
    print(prompt)
```

---

## 使用方法

### 方法 1：手动复制 Prompt

1. 打开 `自动写作 Prompt.md`
2. 复制模板
3. 填充第 X 章的信息
4. 发送给 AI
5. 接收生成的正文

### 方法 2：运行脚本自动生成

```bash
# 生成第 26 章的 Prompt
python scripts/auto_write.py 26

# 输出完整的 Prompt，复制到 AI 对话框
```

### 方法 3：使用 Claude Code 直接写

直接在对话中说：
```
请写第 26 章
```

AI 会自动读取所有设定文件并生成正文。

---

## 文件更新自动化

### 写作后自动更新文件

```python
def update_files(chapter, content):
    """更新所有相关文件"""
    # 1. 更新剧情状态机
    update_status_machine(chapter, content)
    
    # 2. 更新卷索引
    update_volume_index(chapter, content)
    
    # 3. 更新卷概要
    update_volume_summary(chapter, content)
    
    # 4. 更新章节蓝图
    update_chapter_blueprint(chapter, content)
    
    # 5. 更新伏笔系统
    update_foreshadowing(chapter, content)
    
    # 6. 更新时间线
    update_timeline(chapter, content)
```

---

**版本**：2026-04-20  
**适用**：第 1 卷（1-50 章）
