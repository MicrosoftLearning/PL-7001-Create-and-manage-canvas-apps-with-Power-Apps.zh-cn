---
lab:
  title: 实验室 5：外部数据
  module: 'Module 5: Work with external data in a Power Apps canvas app'
---

# 练习实验室 5 - 外部数据

在此实验室中，你将添加一个外部数据源。

## 要学习的知识

- 如何将 SharePoint 列表添加到画布应用
- 如何使用集合
- 如何使用 Patch
- 如何使用 Office365Users 连接器

## 概要实验室步骤

- 创建用于预定的 SharePoint 列表
- 将 SharePoint 列表添加为库
- 存储从库中选定的记录
- 使用 Patch 设置预订请求的决定
- 使用 Office365User 连接器显示用户的详细信息。
  
## 先决条件

- 必须已完成“**实验室 4：生成 UI”**

## 详细步骤

## 练习 1 - 创建 SharePoint 列表

### 任务 1.1 创建 SharePoint 网站

1. 在 [Power Apps 创建者门户](https://make.powerapps.com)中，选择浏览器窗口左上角的“**应用启动器**”，然后选择“**OneDrive**”。

1. 在 SharePoint 中，选择“**+创建网站**”。

1. 依次选择“**团队网站**”、“**标准团队** ”、“**使用模板**”。

1. 输入`Pet boarding`作为**网站名称**，然后选择“**下一步**”。

1. 选择**创建站点**。

1. 选择“完成”。

### 任务 1.2 创建 SharePoint 列表

1. 在 SharePoint 网站中，依次选择“**+ 新建**”、“**列表**”。

    ![新 SharePoint 列表的屏幕截图。](../media/new-sharepoint-list.png)

1. 选择“**空白列表**”

1. 输入`Bookings`作为“**名称**”，然后选择“**创建**”。

1. 依次选择“**+添加列**、“**文本**”、“**下一步**”。

1. 在“**创建列**”窗格中，输入或选择以下值：

   1. 名称：`Pet Name`
   1. 数据类型：**单行文本**

1. 选择“保存”。

1. 依次选择“**添加列**、“**文本**”、“**下一步**”。

1. 在“**创建列**”窗格中，输入或选择以下值：

   1. 名称：`Owner Name`
   1. 数据类型：**单行文本**

1. 选择“保存”。

1. 依次选择“**添加列**、“**日期和时间**”、“**下一步**”。

1. 在“**创建列**”窗格中，输入或选择以下值：

   1. 名称：`Start Date`
   1. 数据类型：**日期和时间**

1. 选择“保存”。

1. 依次选择“**添加列**、“**日期和时间**”、“**下一步**”。

1. 在“**创建列**”窗格中，输入或选择以下值：

   1. 名称：`End Date`
   1. 数据类型：**日期和时间**

1. 选择“保存”。

1. 复制 SharePoint 网站的 URL 的第一部分，例如`https://m365x99999999.sharepoint.com/sites/Petboarding/`

## 练习 2 - 将 SharePoint 列表添加到画布应用

### 任务 2.1 - 编辑应用

1. 导航到 Power Apps Maker 门户 <https://make.powerapps.com>。

1. 确保你位于 **Dev One** 环境中。

1. 从左侧菜单中选择“**应用**”选项卡。

1. 选择 **“预订请求”应用**，选择“命令”（“**...**”），然后选择 **“编辑”>“在新选项卡中编辑”**。

### 任务 2.2 - 将 SharePoint 添加为数据源

1. 在应用创作菜单中，选择**数据**。

1. 选择“**添加数据**”旁边的下拉插入符，然后在“**搜索**”中输入 `SharePoint`。

    ![选择 SharePoint 作为数据源的屏幕截图。](../media/studio-data-sharepoint.png)

1. 选择**SharePoint**。

1. 选择“**直接连接（云服务）**”，然后选择“**连接**”。

1. 输入之前在本实验室中创建的 SharePoint 网站的 URL

    ![连接到 SharePoint 网站的屏幕截图。](../media/select-sharepoint-site.png)

1. 选择“连接” 。

1. 选择“**预定**”。

    ![连接到 SharePoint 列表的屏幕截图。](../media/select-sharepoint-list.png)

1. 选择“连接” 。

### 任务 2.3 - 为 SharePoint 列表添加库

1. 在应用创作菜单中，选择“**插入 (+)**”。

1. 选择**垂直库**。

1. 为数据源选择“**预定**”。

1. 为“**布局**”选择“**标题和副标题**”。

1. 选择“**字段**”旁边的“**已选择 6 个**”

1. 为“**标题**”选择“**决策**”。

1. 为“**副标题**”选择“**开始日期**”。

1. 关闭数据窗格。

1. 在应用创作菜单中，选择“**树状视图**”。

1. 将库重命名为 `BookingList`。

1. 按如下方式设置库的属性：

   1. X=`1000`
   1. Y=`80`
   1. Height=`575`
   1. Width=`250`

## 练习 3 – 集合

### 任务 3.1 创建集合

1. 在应用创作菜单中，选择“**树状视图**”。

1. 展开 **BookingRequestList**。

1. 选择“**NextArrow**”。

1. 将 NextArrow 的“**OnSelect**”属性设置为：

    ```powerappsfl
    Collect(colRequests, ThisItem)
    ```

1. 在应用创作菜单中，选择“**树状视图**”。

1. 选择“**应用**”对象。

1. 将 NextArrow 的“**OnSelect**”属性设置为：

    ```powerappsfl
    Clear(colRequests)
    ```

## 练习 4 – 修补程序

### 任务 4.1 拒绝预订请求

1. 在应用创作菜单中，选择“**树状视图**”。

1. 选择 **BookingRequestList**。

1. 选择库控件左上角的“**铅笔**”图标。

    ![编辑库的屏幕截图。](../media/edit-gallery.png)

1. 在应用创作菜单中，选择“**插入 (+)**”。

1. 展开“**图标**”。

1. 选择“阻止”。 该图标将添加到库中的每一行。

    ![编辑库的屏幕截图。](../media/icon-added-gallery.png)

1. 按如下所示设置图标的属性：

   1. X=`150`
   1. Y=`40`
   1. Height=`30`
   1. Width=`30`

1. 在应用创作菜单中，选择“**树状视图**”。

1. 将图标重命名为“`DeclineIcon`”。

1. 将 **DeclineIcon** 的 **OnSelect** 属性设置为：

    ```powerappsfl
    Patch('Booking Requests', ThisItem, {Decision: 'Decision (Booking Requests)'.Declined})
    ```

## 练习 5 – Office 365 用户

### 任务 5.1 将 Office 365 用户添加为数据源

1. 在应用创作菜单中，选择**数据**。

1. 选择“**添加数据**”旁边的下拉插入符，然后在“**搜索**”中输入 `Office 365`。

1. 选择 **Office 365 用户**。

1. 选择“连接” 。

### 任务 5.2 显示用户的国家/地区

1. 单击空白画布上库的外部。

1. 在应用创作菜单中，选择“**插入 (+)**”。

1. 选择**文本标签**。

1. 将标签拖到 UserLabel 旁边的屏幕右上角。

1. 在应用创作菜单中，选择“**树状视图**”。

1. 将标签重命名为 `UserDetailsLabel`。

1. 将 **UserDetailsLabel** 的 **OnSelect** 属性设置为：

    ```powerappsfl
    Office365Users.MyProfile().Country
    ```

1. 选择 Power Apps Studio 右上角的“**保存**”。

1. 选择命令栏左上角的“**<- 返回**”按钮，然后选择“**退出**”以退出应用。