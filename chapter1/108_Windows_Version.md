# Как да проверим коя е версията на операционната система?

За да проверите текущата версия на операционната система Windows използвайте клавишна комбинация **Windows Key + R** _\(Фиг. 1.18\)_. В появилия се диалогов прозорец Run запишете команда **winver** _\(Фиг. 1.19\)_ и натиснете **Enter**. В резултат ще видите екран About Windows _\(Фиг. 1.20\)_ в който се вижда текущата версията на операционната система.

![](/images/118_Windows__key_plus_R.png)

_Фиг. 1.18. Клавишна комбинация Windows Key + R_

![](/images/119_Run.png)

_Фиг. 1.19. Диалогов прозорец RUN_

![](/images/120_WinVer.png)

_Фиг. 1.20. Версия на операционната система Windows_

{% hint style='info' %}
#### Бележка
Ако искате да смените името и/или организацията стартирайте **Registry Editor**
```
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion
```
Променете стойностите на полетата:
- RegisteredOwner
- RegisteredOrganization  
{% endhint %}



