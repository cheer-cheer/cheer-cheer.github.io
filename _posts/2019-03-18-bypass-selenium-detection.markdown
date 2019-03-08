---
layout: post
title:  "WebDriver - 绕过淘宝的反爬虫检测机制"
date:   2018-03-18 23:34:05 +0800
categories: webdriver IT 爬虫
---

```javascript
Object.defineProperty(navigator, 'webdriver', { 
  get: () => undefined 
})
```


```csharp
public static object AddScriptToEvaluateOnNewDocument(this IWebDriver driver, 
    string script)
{
    var chrome = driver as ChromeDriver;
    if (chrome == null)
    {
        return null;
    }
    if (string.IsNullOrEmpty(script))
    {
        return null;
    }

    const string cmd = "Page.addScriptToEvaluateOnNewDocument";
    var parameters = new Dictionary<string, object>(1)
    {
        { "source", script }
    };

    return chrome.ExecuteChromeCommandWithResult(cmd, parameters);
}
```