---
title: duilib 基础代码框架
date: 2025-06-22
categories:
  - duilib
tags:
  - duilib
  - Windows
---

实际上的代码配置上需要不了多少的东西，真正难搞的是 duilib 内部的逻辑，所以这里先保证实现使用 duilib 库，直接粘贴一部分代码。

下面是主函数中的代码：

```cpp
int APIENTRY WinMain(HINSTANCE hInstance, HINSTANCE /*hPrevInstance*/, LPSTR /*lpCmdLine*/, int nCmdShow)
{
    CPaintManagerUI::SetInstance(hInstance); // duilib 配置句柄
    CPaintManagerUI::SetResourcePath(CPaintManagerUI::GetInstancePath() + _T("skin")); // 设置资源目录
    CPaintManagerUI::SetResourceZip(_T("360SafeRes.zip")); // 这里是可选的，也亦可使用目录
    // 或者可以改成直接导向资源的目录不使用压缩包
    // CPaintManagerUI::SetResourcePath(CPaintManagerUI::GetInstancePath() + _T("skin//360SafeRes"));

    HRESULT Hr = ::CoInitialize(NULL); // 初始化当前线程上的 COM 库，并将并发模型标识为单线程单元 (STA)。
    if (FAILED(Hr)) return 0;

    C360SafeFrameWnd* pFrame = new C360SafeFrameWnd();
    if (pFrame == NULL) return 0;
    pFrame->Create(NULL, _T("360安全卫士"), UI_WNDSTYLE_FRAME, 0L, 0, 0, 800, 572); // 创建窗口
    pFrame->CenterWindow(); // 窗口居中
    ::ShowWindow(*pFrame, SW_SHOW); // 展示窗口

    CPaintManagerUI::MessageLoop(); // 消息循环

    ::CoUninitialize(); // 关闭当前线程上的 COM 库，卸载线程加载的所有 DLL，释放线程维护的任何其他资源，并强制关闭线程上的所有 RPC 连接。
    return 0;
}
```
