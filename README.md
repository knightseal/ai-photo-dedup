# AI Photo Deduplicator - 智能重复照片清理工具

基于 perceptual hashing 和 AI 视觉分析的重复照片检测与清理工具。

## 功能特性

- **🔍 智能检测**：使用 pHash + dHash 感知哈希算法检测相似图片
- **🤖 AI 辅助**：集成 CLIP 模型进行语义相似度分析
- **⚡ 高效处理**：支持多线程并行处理，支持百万级图片库
- **🖼️ 格式支持**：JPG, PNG, HEIC, RAW, WebP 等主流格式
- **📊 可视化报告**：生成 HTML 报告展示重复图片组
- **🛡️ 安全操作**：默认模拟模式，确认后才执行删除

## 快速开始

```bash
# 安装依赖
pip install -r requirements.txt

# 扫描指定目录（模拟模式，不实际删除）
python photo_dedup.py scan ~/Pictures --output report.html

# 执行清理（会实际移动重复文件到回收站）
python photo_dedup.py clean ~/Pictures --execute
```

## 工作原理

1. **扫描阶段**：递归遍历目录，提取图片特征
2. **哈希计算**：计算感知哈希值作为相似度基础
3. **聚类分组**：使用汉明距离阈值分组相似图片
4. **AI 精筛**：对疑似重复组使用 CLIP 进行语义验证
5. **质量评估**：基于分辨率、文件大小、EXIF 信息选择最佳保留项
6. **执行清理**：移动重复项到隔离目录（可恢复）

## 项目结构

```
├── photo_dedup.py          # 主程序入口
├── core/
│   ├── scanner.py          # 文件扫描器
│   ├── hasher.py           # 哈希计算
│   ├── grouper.py          # 相似图片分组
│   ├── ai_analyzer.py      # AI 语义分析
│   └── cleaner.py          # 清理执行器
├── utils/
│   ├── image_utils.py      # 图片处理工具
│   └── report_generator.py # 报告生成
├── tests/
└── requirements.txt
```

## License

MIT
