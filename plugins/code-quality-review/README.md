# Code Quality Review

专业的代码质量检测工具，提供项目级别的质量评估、详细测试报告、综合评分和优化修改计划。

## 快速开始

### 基本使用

```bash
# 分析项目质量
kiro quality-review analyze --path ./src

# 生成完整报告 (自动添加时间戳)
kiro quality-review report --format html

# 对比两个版本
kiro quality-review compare --baseline main --branch feature/new

# 查看改进计划
kiro quality-review plan --priority high

# 监控趋势
kiro quality-review trends --days 30
```

### 配置项目

```bash
# 1. 复制配置模板
cp plugins/code-quality-review/config.example.yml .kiro/quality-review.yml

# 2. 根据项目需求调整配置

# 3. 运行检测
kiro quality-review analyze
```

## 核心功能

### 1. 多维度质量评估

**6个质量维度:**
- **可维护性 (20%)** - 复杂度、重复率、代码行数
- **可靠性 (25%)** - 错误处理、异常捕获、空值检查
- **安全性 (25%)** - 漏洞扫描、敏感信息检测、输入验证
- **性能 (15%)** - 算法复杂度、查询优化、内存效率
- **可测试性 (10%)** - 测试覆盖率、Mock使用、依赖注入
- **文档 (5%)** - API文档、代码注释、README

### 2. 综合评分系统

```
总分 = 可维护性(20%) + 可靠性(25%) + 安全性(25%) + 
       性能(15%) + 可测试性(10%) + 文档(5%)
```

**等级划分:**
- **A (90-100)** - 优秀
- **B (80-89)** - 良好
- **C (70-79)** - 中等
- **D (60-69)** - 较差
- **F (<60)** - 不合格

### 3. 详细报告生成

**报告内容:**
- 质量概览 - 总体评分、各维度评分、关键指标
- 详细分析 - 问题分类、代码示例、影响范围
- 修改计划 - 优先级排序、工作量评估、实施路线图
- 趋势分析 - 历史数据对比、改进趋势、未来预测

**输出格式:**
- HTML (交互式仪表板)
- JSON (数据格式)
- Markdown (文本格式)

### 4. 报告文件管理

报告文件自动添加时间戳：

```
./quality-reports/
├── quality-report-2024-01-18_09-00-00.html
├── quality-report-2024-01-18_14-30-45.html
├── quality-report-2024-01-19_10-15-30.html
└── ...
```

**文件名配置:**
```yaml
reporting:
  filename:
    pattern: "quality-report-{timestamp}.{format}"
    use_timestamp: true
    timestamp_format: "YYYY-MM-DD_HH-mm-ss"
```

**可用变量:**
- `{timestamp}` - 完整时间戳
- `{date}` - 日期
- `{time}` - 时间
- `{format}` - 报告格式
- `{branch}` - 分支名称
- `{project}` - 项目名称

## 使用场景

### 场景1: 项目初期评估
```
质量检测 → 基线建立 → 改进计划制定 → 团队讨论
```

### 场景2: 持续质量监控
```
定期检测 → 趋势分析 → 预警提醒 → 改进跟踪
```

### 场景3: 代码审查辅助
```
PR提交 → 质量检测 → 审查建议 → 合并决策
```

### 场景4: 重构前后对比
```
重构前检测 → 重构 → 重构后检测 → 效果评估
```

## 集成方式

### IDE集成
- 实时质量提示
- 问题高亮显示
- 快速修复建议
- 质量趋势面板

### CI/CD集成

```yaml
# GitHub Actions 示例
- name: Code Quality Review
  run: kiro quality-review analyze --format json --output quality.json

- name: Quality Gate
  run: |
    SCORE=$(jq '.overall_score' quality.json)
    if (( $(echo "$SCORE < 70" | bc -l) )); then
      echo "Quality score too low: $SCORE"
      exit 1
    fi
```

### 命令行使用

```bash
# 分析项目
kiro quality-review analyze --path ./src

# 生成报告
kiro quality-review report --format html --output report.html

# 对比版本
kiro quality-review compare --baseline main --branch feature

# 查看改进计划
kiro quality-review plan --format markdown --output plan.md

# 监控趋势
kiro quality-review trends --days 30 --format html
```

## 配置指南

### 基本配置

```yaml
quality-review:
  enabled: true
  
  # 检测范围
  scope:
    include:
      - src/**/*.ts
      - src/**/*.js
    exclude:
      - "**/*.test.ts"
      - node_modules/**
  
  # 评分权重
  weights:
    maintainability: 0.20
    reliability: 0.25
    security: 0.25
    performance: 0.15
    testability: 0.10
    documentation: 0.05
  
  # 质量阈值
  thresholds:
    complexity_max: 10
    duplication_max: 5
    unit_test_coverage_min: 80
    security_score_min: 90
```

详见 `config.example.yml`

## 改进计划优先级

| 优先级 | 类型 | 示例 | 收益 | 难度 |
|--------|------|------|------|------|
| 1 | 紧急改进 | 安全漏洞、系统稳定性 | 高 | 中等 |
| 2 | 重点改进 | 测试覆盖率、复杂度 | 高 | 中等 |
| 3 | 常规改进 | 代码重复、文档 | 中等 | 中等 |
| 4 | 持续改进 | 代码风格、最佳实践 | 低 | 低 |

## 最佳实践

1. **定期检测** - 每周或每个迭代进行一次
2. **设置基线** - 建立项目的质量基线
3. **优先改进** - 按优先级逐步改进
4. **团队对齐** - 与团队讨论质量目标
5. **持续监控** - 建立质量监控仪表板
6. **文档维护** - 保持文档与代码同步

## 常见问题

**Q: 如何快速提升评分?**  
A: 关注权重最高的维度 (可靠性、安全性)，优先处理Critical问题，提升测试覆盖率。

**Q: 如何处理技术债?**  
A: 量化技术债、优先级排序、逐步偿还、防止新增。

**Q: 如何与CI/CD集成?**  
A: 在构建流程中添加检测步骤、设置质量门禁、生成报告、配置通知。

**Q: 支持哪些语言?**  
A: JavaScript/TypeScript、Python、Java、C#、Go、Rust、PHP、Ruby、C++。

## 支持的工具

- **静态分析**: ESLint, Pylint, Checkstyle
- **代码覆盖率**: Jest, Pytest, JaCoCo
- **质量平台**: SonarQube, CodeClimate
- **依赖扫描**: Snyk, Dependabot
- **安全检测**: OWASP, Bandit

## 相关资源

- [POWER.md](./POWER.md) - 功能概述
- [config.example.yml](./config.example.yml) - 配置示例
- [agents/quality-analyzer.md](./agents/quality-analyzer.md) - AI Agent定义
- [commands/quality-report.md](./commands/quality-report.md) - 命令定义
