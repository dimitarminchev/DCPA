# Как да проверим коя е версията на операционната система?

За да проверите текущата версия на операционната система Windows използвайте клавишна комбинация Windows Key + R \(Фиг. 18\). В появилия се диалогов прозорец RUN запишете команда WINVER \(Фиг. 19\) и натиснете Enter. В резултат ще видите екран About Windows \(Фиг. 20\) в който се вижда текущата версията на операционната система.

![](/images/18_Windows__key_plus_R.png)

_Фиг.18. Клавишна комбинация Windows Key + R_

![](/images/19_run.png)

_Фиг.19. Диалогов прозорец RUN_

![](/images/20_WinVer.png)

_Фиг.20. Версия на операционната система Windows_

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



