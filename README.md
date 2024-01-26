## Rime 鼠须管（Squirrel）朙月拼音、小鹤双拼配置自用

去掉输入方案：自然码

去掉功能：「Shift，切换中英文」。已使用 Shift 来切换中英文输入法

修改动态日期时间：修改双拼下的缩写，增加日期和时间的组合展示

```
function date_translator(input, seg)
    if (input == "date") then
        --- Candidate(type, start, end, text, comment)
        yield(Candidate("date", seg.start, seg._end, os.date("%Y-%m-%d"), ""))
        yield(Candidate("date", seg.start, seg._end, os.date("%Y年%m月%d日"), ""))
        yield(Candidate("date", seg.start, seg._end, os.date("%m-%d"), ""))
        yield(Candidate("date", seg.start, seg._end, os.date("%Y/%m/%d"), ""))
    end
    if (input == "time") then
        --- Candidate(type, start, end, text, comment)
        yield(Candidate("time", seg.start, seg._end, os.date("%H:%M"), ""))
        yield(Candidate("time", seg.start, seg._end, os.date("%H:%M:%S"), ""))
    end
    if (input == "datetime") then
        --- Candidate(type, start, end, text, comment)
        yield(Candidate("datetime", seg.start, seg._end, os.date("%Y-%m-%d %H:%M:%S"), ""))
        yield(Candidate("datetime", seg.start, seg._end, os.date("%Y年%m月%d日 %H:%M:%S"), ""))
    end
    if (input == "week") then
        local weakTab = {'日', '一', '二', '三', '四', '五', '六'}
        yield(Candidate("week", seg.start, seg._end, "周"..weakTab[tonumber(os.date("%w")+1)], ""))
        yield(Candidate("week", seg.start, seg._end, "星期"..weakTab[tonumber(os.date("%w")+1)], ""))
        yield(Candidate("week", seg.start, seg._end, "礼拜"..weakTab[tonumber(os.date("%w")+1)], ""))
    end
end
```

增加常用语：

```
「	zkh
」	ykh
```

修改特定程序原定英文的全部改为中文（删除了不生效那就全改false）：统一使用 Input Source Pro 来控制

```
  # 特定App默认中/英文输入
  app_options:
    com.apple.Spotlight: # 聚焦搜索
      ascii_mode: false             # true默认英文,false默认中文
    com.runningwithcrayons.Alfred: # alfred
      ascii_mode: false
    com.apple.Terminal: # 终端
      ascii_mode: false
    com.microsoft.VSCode: # Visual Studio Code
      ascii_mode: false
    com.tencent.Lemon: # 腾讯柠檬
      ascii_mode: false
    com.apple.dt.Xcode: # Xcode
      ascii_mode: false
    com.nektony.App-Cleaner-SII: # App Cleaner & Uninstaller
      ascii_mode: false
    com.xunyong.hapigo: # hapigo
      ascii_mode: false
    com.termius-dmg.mac: # termius
      ascii_mode: false
    com.raycast.macos: # Raycast
      ascii_mode: false
    com.jetbrains.intellij: # idea
      ascii_mode: false
```
