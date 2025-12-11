# How to check the operating system version?

To check the current version of Windows, use the keyboard shortcut **Windows Key + R** _(Fig. 1.18)_. In the Run dialog that appears, type the command **winver** _(Fig. 1.19)_ and press **Enter**. The About Windows dialog _(Fig. 1.20)_ will display the current operating system version.

![](/images/118_Windows__key_plus_R.png)

_Fig. 1.18. Keyboard shortcut Windows Key + R_

![](/images/119_Run.png)

_Fig. 1.19. RUN dialog_

![](/images/120_WinVer.png)

_Fig. 1.20. Windows operating system version_

{% hint style='info' %}
#### Note
If you want to change the registered owner or organization name, open the **Registry Editor** and navigate to:
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion
```
Modify the values for the fields:
- RegisteredOwner
- RegisteredOrganization
{% endhint %}



