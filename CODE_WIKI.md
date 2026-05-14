# DW 预约系统 - Code Wiki

## 项目概述

DW 预约系统是一个轻量级的在线预约管理系统，采用纯前端技术栈构建，使用 Supabase 作为后端数据库服务。系统支持用户查看日历、预约特定时段，并提供管理员后台进行预约管理。

## 目录结构

```
reserve/
├── index.html          # 主页面文件
├── css/
│   └── styles.css      # 样式文件
└── js/
    ├── config.js       # 配置文件
    └── app.js          # 应用主逻辑
```

## 核心文件说明

### 1. [index.html](file:///Users/dingwei/Documents/GitHub/reserve/index.html)

主页面文件，包含所有的 UI 结构和组件。

**主要组件**：
- 加载界面
- 头部导航
- 日历网格
- 预约模态框
- 管理员登录模态框
- 确认对话框
- 日期详情模态框
- 管理员页面

### 2. [css/styles.css](file:///Users/dingwei/Documents/GitHub/reserve/css/styles.css)

完整的样式文件，使用 CSS 变量定义主题色，采用温暖的教育类配色方案。

**核心设计特点**：
- 响应式设计，支持移动端
- 使用 CSS 变量统一管理样式
- 柔和的过渡动画效果
- 清晰的状态指示

### 3. [js/config.js](file:///Users/dingwei/Documents/GitHub/reserve/js/config.js)

配置文件，包含系统的关键配置参数。

**配置项**：
- `SUPABASE_URL` - Supabase 项目地址
- `SUPABASE_ANON_KEY` - Supabase 匿名密钥
- `TABLE` - 数据库表名
- `ADMIN_PWD` - 管理员密码
- `DAYS_AHEAD` - 日历显示天数
- `TIME_SLOTS` - 时间段定义
- `WEEKDAYS` - 中文星期数组
- `MONTHS` - 中文月份数组

### 4. [js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js)

应用主逻辑文件，实现了所有的交互功能。

## 主要功能模块

### 1. 数据通信模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L7-L19)

**核心函数**：
- `supabaseHeaders()` - 生成 Supabase 请求头
- `apiUrl(path)` - 生成 API 请求 URL

### 2. 状态管理

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L21-L25)

**状态变量**：
- `allBookings` - 所有预约记录
- `selectedDate` - 选中的日期
- `selectedTime` - 选中的时段
- `isAdmin` - 是否为管理员状态

### 3. 工具函数

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L27-L47)

**核心函数**：
- `formatDate(date)` - 格式化日期为 YYYY-MM-DD 格式
- `escapeHtml(str)` - HTML 转义防止 XSS
- `getBookingForSlot(dateStr, timeKey)` - 获取某日期某时段的预约
- `validateReason(reason)` - 验证预约事由

### 4. 通知提示模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L49-L78)

**核心函数**：
- `showToast(message, type)` - 显示提示消息
- `showConfirm(title, message, onConfirm)` - 显示确认对话框
- `closeConfirm()` - 关闭确认对话框

### 5. 日历渲染模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L80-L185)

**核心函数**：
- `getDayStatus(dateStr)` - 获取某一天的预约状态
- `renderWeekdayHeaders()` - 渲染星期标题
- `renderCalendar()` - 渲染完整日历

**功能特点**：
- 显示未来 N 天的日历
- 显示每日预约状态（空闲/部分/满）
- 支持点击日期查看详情

### 6. 日期详情模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L187-L233)

**核心函数**：
- `openDateDetailModal(dateStr, dateObj)` - 打开日期详情模态框
- `closeDateDetailModal()` - 关闭日期详情模态框

### 7. 预约管理模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L235-L325)

**核心函数**：
- `openBookModal(dateStr, slot)` - 打开预约模态框
- `closeBookModal()` - 关闭预约模态框
- `submitBooking()` - 提交预约

### 8. 管理员模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L327-L498)

**核心函数**：
- `openAdminLogin()` - 打开管理员登录
- `closeLoginModal()` - 关闭登录模态框
- `verifyAdmin()` - 验证管理员密码
- `showAdminPage()` - 显示管理页面
- `backToHome()` - 返回首页
- `renderAdminStats()` - 渲染统计数据
- `renderAdminList()` - 渲染预约列表
- `requestDelete(id, name, date, timeLabel)` - 请求删除预约
- `deleteBooking(id)` - 删除预约

### 9. 自动清理模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L500-L543)

**核心函数**：
- `cleanupExpiredBookings()` - 自动清理过期 3 天以上的预约

### 10. 数据加载模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L545-L575)

**核心函数**：
- `loadBookings()` - 加载预约数据

### 11. 初始化模块

**文件**：[js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js#L577-L613)

**核心函数**：
- `init()` - 初始化应用

## 数据库结构

**表名**：`bookings`

**字段**：
- `id` - 主键（整数）
- `date` - 预约日期（文本，格式 YYYY-MM-DD）
- `time` - 预约时段（文本）
- `name` - 预约人姓名（文本）
- `reason` - 预约事由（文本）

**唯一约束**：date 和 time 组合唯一，防止重复预约

## 依赖关系

**外部依赖**：
- Supabase REST API - 后端数据库服务
- Google Fonts - Playfair Display 和 Inter 字体

**内部依赖**：
- [js/config.js](file:///Users/dingwei/Documents/GitHub/reserve/js/config.js) 必须在 [js/app.js](file:///Users/dingwei/Documents/GitHub/reserve/js/app.js) 之前加载

## 运行方式

1. 直接在浏览器中打开 [index.html](file:///Users/dingwei/Documents/GitHub/reserve/index.html)
2. 或使用本地服务器（如 VS Code 的 Live Server 插件）运行

## 安全注意事项

- 管理员密码以明文存储在配置文件中，仅供演示使用
- Supabase 匿名密钥暴露在前端，应配合适当的行级安全策略（RLS）使用
- 所有用户输入都进行了 HTML 转义处理，防止 XSS 攻击

## 维护与扩展

### 添加新的时间段

在 [js/config.js](file:///Users/dingwei/Documents/GitHub/reserve/js/config.js#L20-L25) 的 `TIME_SLOTS` 数组中添加新对象：

```javascript
{ key: 'new_slot', label: '新时段', icon: '🎉', time: '00:00-00:00' }
```

### 修改管理员密码

在 [js/config.js](file:///Users/dingwei/Documents/GitHub/reserve/js/config.js#L13) 修改 `ADMIN_PWD` 配置项。

### 调整日历显示天数

在 [js/config.js](file:///Users/dingwei/Documents/GitHub/reserve/js/config.js#L16) 修改 `DAYS_AHEAD` 配置项。
