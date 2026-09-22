---
title: duilib 控件属性配置
date: 2025-05-14
categories:
  - duilib
tags:
  - duilib
  - Windows
---

## 设置图片的透明度

```cpp
// 获取图片控件
CControlUI* pImageCtrl = static_cast<CControlUI*>(m_pm.FindControl(_T("imgTest")));
if (pImageCtrl != NULL) {
    // 设置图片的 Alpha 值为 128，即半透明
    pImageCtrl->SetBkImage(_T("image.png"));
    pImageCtrl->SetBkImageAlpha(128);
}
```
