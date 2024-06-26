# Clicker Mania 2.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим универсално приложение отчитащо броя кликове на потребителя за определено време.

## Start

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. За име на проекта запишете: **Clicker Mania 2.0**.

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<Page
    x:Class="Clicker_Mania_2._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Clicker_Mania_2._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Clicker Mania 2.0 -->
    <StackPanel Background="Lime" Padding="30">
        
        <!-- Title -->
        <TextBlock FontSize="30" Padding="10" HorizontalAlignment="Center" Text="Clicker Mania 2.0" FontWeight="ExtraBlack" />

        <!-- Timer -->
        <TextBlock Text="Timer" FontSize="23" HorizontalAlignment="Center" />
        <TextBlock Name="Timer" Foreground="White" Text="0" FontSize="60" HorizontalAlignment="Center" FontWeight="ExtraBlack" />

        <!-- Clicks -->
        <TextBlock Text="Clicks" FontSize="23" HorizontalAlignment="Center" />
        <TextBlock Name="Clicks" Foreground="White" Text="0" FontSize="60" HorizontalAlignment="Center" FontWeight="ExtraBlack" />

        <!-- Clicks Per Minute -->
        <TextBlock Text="Clicks Per Minute" FontSize="23" HorizontalAlignment="Center" />
        <TextBlock Name="CPM" Foreground="White" Text="0" FontSize="60" HorizontalAlignment="Center" FontWeight="ExtraBlack" />
        
        <!-- Button -->
        <Button Content="Click" Padding="50 10 50 10" HorizontalAlignment="Center" FontSize="32" Click="Button_Click" />
   
    </StackPanel>
</Page>

```

Изглед от дизайна на потребителският интерфейс \(XAML\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/37_Clicker_Mania_2.0_UI.png)

_Фиг. 37. Изглед от дизайна на потребителският интерфейс_

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;

namespace Clicker_Mania_2._0
{
    /// <summary>
    /// Business Logic (BL): Clicker Mania 2.0
    /// </summary>
    public sealed partial class MainPage : Page
    {
        // Dispacher Timer
        private DispatcherTimer timer = new DispatcherTimer();

        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
            // Timer
            timer.Interval = new TimeSpan(0, 0, 1);
            timer.Tick += Timer_Tick;
            timer.Start();
        }

        // Timer Tick Event Handler
        private void Timer_Tick(object sender, object e)
        {
            int T = int.Parse(Timer.Text);
            Timer.Text = (++T).ToString();
            // clicks Per Minute
            CPM.Text = (float.Parse(Clicks.Text) / float.Parse(Timer.Text) * 60).ToString("N2");
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            int N = int.Parse(Clicks.Text);
            Clicks.Text = (++N).ToString();
        }
    }
}
```

Изглед от бизнес логиката \(C\#\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/38_Clicker_Mania_2.0_BL.png)

_Фиг. 38. Изглед от бизнес логиката на разработваното приложение_

## Demo 

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/39_Clicker_Mania_2.0_Run.png)

_Фиг.39 Универсално приложение отчитащо броя кликове на потребителя за определено време_

