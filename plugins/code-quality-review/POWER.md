# Code Quality Review Plugin

专业的代码质量检测工具，提供项目级别的质量评估、详细测试报告、综合评分和优化修改计划。

## 核心能力

- **多维度质量评估**: 可维护性、可靠性、安全性、性能、可测试性、文档完整性
- **综合评分系统**: 0-100分制，A-F等级划分
- **详细报告生成**: HTML、JSON、Markdown多种格式，自动时间戳命名
- **改进计划制定**: 优先级排序，包含工作量和收益评估
- **趋势分析**: 历史数据对比，预测未来质量

## 6个质量维度

| 维度 | 权重 | 关键指标 | 目标 |
|------|------|---------|------|
| 可维护性 | 20% | 复杂度、重复率、代码行数 | 复杂度<10, 重复率<5% |
| 可靠性 | 25% | 错误处理、异常捕获、空值检查 | 覆盖率>80% |
| 安全性 | 25% | 漏洞、敏感信息、输入验证 | 评分>90 |
| 性能 | 15% | 算法复杂度、查询优化、内存效率 | 无N+1查询 |
| 可测试性 | 10% | 测试覆盖率、Mock使用、依赖注入 | 覆盖率>80% |
| 文档 | 5% | API文档、注释、README | 覆盖率>90% |

## 评分体系

```
总分 = 可维护性(20%) + 可靠性(25%) + 安全性(25%) + 
       性能(15%) + 可测试性(10%) + 文档(5%)
```

| 等级 | 分数 | 含义 |
|------|------|------|
| A | 90-100 | 优秀 |
| B | 80-89 | 良好 |
| C | 70-79 | 中等 |
| D | 60-69 | 较差 |
| F | <60 | 不合格 |

## 快速开始

```bash
# 分析项目
kiro quality-review analyze

# 生成报告 (自动添加时间戳)
kiro quality-review report --format html

# 对比版本
kiro quality-review compare --baseline main --branch feature

# 查看改进计划
kiro quality-review plan --priority high

# 监控趋势
kiro quality-review trends --days 30
```

## 报告文件管理

报告文件自动添加时间戳，便于版本管理和历史追踪：

```
./quality-reports/
├── quality-report-2024-01-18_09-00-00.html
├── quality-report-2024-01-18_14-30-45.html
├── quality-report-2024-01-19_10-15-30.html
└── ...
```

### 文件名配置

```yaml
reporting:
  filename:
    pattern: "quality-report-{timestamp}.{format}"
    use_timestamp: true
    timestamp_format: "YYYY-MM-DD_HH-mm-ss"
```

### 可用变量

- `{timestamp}` - 完整时间戳 (YYYY-MM-DD_HH-mm-ss)
- `{date}` - 日期 (YYYY-MM-DD)
- `{time}` - 时间 (HH-mm-ss)
- `{format}` - 报告格式 (html/json/markdown)
- `{branch}` - 分支名称
- `{project}` - 项目名称

## 改进优先级

| 优先级 | 类型 | 示例 | 收益 | 难度 |
|--------|------|------|------|------|
| 1 | 紧急改进 | 安全漏洞、系统稳定性 | 高 | 中等 |
| 2 | 重点改进 | 测试覆盖率、复杂度 | 高 | 中等 |
| 3 | 常规改进 | 代码重复、文档 | 中等 | 中等 |
| 4 | 持续改进 | 代码风格、最佳实践 | 低 | 低 |

## 支持的语言

JavaScript/TypeScript, Python, Java, C#, Go, Rust, PHP, Ruby, C++

## 依赖工具

- ESLint, Pylint, Checkstyle
- Jest, Pytest, JaCoCo
- SonarQube, CodeClimate
- Snyk, Dependabot
- OWASP, Bandit

## 最佳实践

1. **定期检测** - 每周或每个迭代
2. **设置基线** - 建立质量基线
3. **优先改进** - 按优先级逐步改进
4. **团队对齐** - 讨论质量目标
5. **持续监控** - 建立质量仪表板
6. **文档维护** - 保持文档同步
