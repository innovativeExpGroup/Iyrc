# Iyrc

墨韵读书会 —— 图书管理系统

## 简介

课程设计项目，采用三层架构：

- `IyrcUI` 使用 Python 的 Tkinter 库构建，是负责处理用户交互的边界类
- `IyrcManager` 是控制类，负责控制业务流程
- `IyrcDB` 使用 SQLite 构建，是存储相关信息的实体类

## 目录结构

```
Iyrc/
├── src/
│   ├── IyrcUI.py        边界类：Tkinter 图形界面，程序入口
│   ├── IyrcManager.py   控制类：业务流程
│   ├── IyrcDB.py        实体类：SQLite 建表与数据访问
│   ├── Book.py          书籍实体
│   ├── Blog.py          博客实体
│   └── User.py          用户实体
├── .gitignore
├── LICENSE
└── README.md
```

## 运行

```bash
python src/IyrcUI.py
```

- 依赖：仅 Python 标准库（`tkinter`、`sqlite3`），无需 `pip install`
- 首次运行会在**当前工作目录**自动创建空的 `Iyrc.db`，四张表由 `IyrcDB.py` 中的 `CREATE TABLE IF NOT EXISTS` 建立
- 数据库文件已被 `.gitignore` 排除，不进版本库；如需自带测试数据，请自行放置 `Iyrc.db`

## 数据库表结构

USER Table
用户表，存储用户相关信息

| Field     | Type    | Constraints |
|-----------|---------|-------------|
| ID        | INT     | PRIMARY KEY, NOT NULL |
| USERNAME  | TEXT    | NOT NULL    |
| PASSWORD  | TEXT    | NOT NULL    |
| EMAIL     | TEXT    |             |
| TYPE      | TEXT    | NOT NULL    |

BOOK Table
书籍表，存放书籍相关信息

| Field     | Type    | Constraints |
|-----------|---------|-------------|
| ID        | INT     | PRIMARY KEY, NOT NULL |
| NAME      | TEXT    | NOT NULL    |
| AUTHOR    | TEXT    | NOT NULL    |
| TEXT      | TEXT    |             |

BLOG Table
博客表，存储博客相关信息

| Field        | Type    | Constraints              |
|--------------|---------|--------------------------|
| ID           | INT     | PRIMARY KEY, NOT NULL     |
| TITLE        | TEXT    | NOT NULL                 |
| AUTHOR       | TEXT    | NOT NULL                 |
| CREATE_TIME  | INT     | NOT NULL                 |
| CHANGE_TIME  | INT     | NOT NULL                 |
| TEXT         | TEXT    |                          |

USERBOOK Table
用户书籍表，存储用户的书架信息

| Field     | Type    | Constraints |
|-----------|---------|-------------|
| USERID    | TEXT    | NOT NULL    |
| BOOKID    | TEXT    | NOT NULL    |
