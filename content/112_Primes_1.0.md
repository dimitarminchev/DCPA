# Primes 1.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим универсално приложение за генериране на редица от прости числа.

{% hint style='info' %}
#### Информация
Просто число е естествено число, по-голямо от 1, което не е произведение на две по-малки естествени числа.
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/Prime_number)
{% endhint %}


## Start

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. За име на проекта запишете: **Primes 1.0**.

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<Page
    x:Class="Primes_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Primes_1._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Primes 1.0 -->
    <StackPanel Background="Yellow" Padding="50">

        <!-- Title -->
        <TextBlock Text="Primes 1.0" FontSize="40" />
        
        <!-- Limit -->
        <TextBlock Text="Limit" FontSize="20" />
        <TextBox Name="boxLimit" Text="1000" FontSize="20" />
        <Button Content="Generate" Margin="0 10 0 10" Padding="20 10 20 10" FontSize="20"  Click="Button_Click" />
        
        <!-- Numbers -->
        <ListBox Name="boxNumbers" Height="400" FontSize="20" />
        
    </StackPanel>
</Page>
```

Изглед от дизайна на потребителският интерфейс \(XAML\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/29_Primes_1.0_UI.png)

_Фиг. 29. Изглед от дизайна на потребителският интерфейс_

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;

namespace Primes_1._0
{
    /// <summary>
    /// Business Logic (BL): Primes 1.0
    /// </summary>
    public sealed partial class MainPage : Page
    {
        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
        }

        // Button Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            int limit = int.Parse(boxLimit.Text);
            for (int k = 2; k < limit; k++)
            {
                bool prime = true;
                for (int j = 2; j < k; j++) if (k % j == 0) prime = false;
                if (prime) boxNumbers.Items.Add(k);
            }
        }
    }
}
```

Изглед от бизнес логиката \(C\#\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/30_Primes_1.0_BL.png)

_Фиг. 30. Изглед от бизнес логиката на разработваното приложение_

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/31_Primes_1.0_Run.png)

_Фиг. 31. Универсално приложение за генериране на редица от прости числа._

