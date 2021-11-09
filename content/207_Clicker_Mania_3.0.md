# Clicker Mania 3.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим мулти-платформено мобилно приложение отчитащо броя кликове на потребителя за определено време.

## Start

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**. 
3. За име на проекта запишете: **Clicker Mania 3.0**.

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Clicker_Mania_3._0.MainPage">

    <!-- User Interface (UI): Clicker Mania 3.0 -->
    <StackLayout Padding="20" BackgroundColor="Lime">

        <!-- Title -->
        <Label Text="Clicker Mania 3.0" FontSize="Large" />

        <!-- Timer -->
        <Label Text="Timer" />
        <Entry x:Name="Timer" Text="0" />

        <!-- Clicks -->
        <Label Text="Clicks" />
        <Entry x:Name="Clicks" Text="0" />

        <!-- Clicks Per Minute -->
        <Label Text="Clicks Per Minute" />
        <Entry x:Name="CPM" Text="0" />

        <!-- Button -->
        <Button Text="Click" Clicked="OnButtonClicked" />
        
    </StackLayout>
</ContentPage>
```

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using Xamarin.Forms;

namespace Clicker_Mania_3._0
{
    // Business Logic (BL): Clicker Mania 3.0
    public partial class MainPage : ContentPage
    {
        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
			
            // Timer
            Device.StartTimer(TimeSpan.FromSeconds(1), TimerTick);
        }

        // Timer Tick Event Handler
        private bool TimerTick()
        {
            int T = int.Parse(this.Timer.Text);
            this.Timer.Text = (++T).ToString();
            // clicks Per Minute
            this.CPM.Text = (float.Parse(this.Clicks.Text) /
            float.Parse(this.Timer.Text) * 60).ToString("N2");
            return true;
        }

        // Button Click Event Handler
        void OnButtonClicked(object sender, EventArgs args)
        {
            int N = int.Parse(this.Clicks.Text);
            this.Clicks.Text = (++N).ToString();
        }
    }
}
```

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/60_Clicker_Mania_3.0.png)

_Фиг.60 Тестване на мултиплатформено мобилно приложение отчитащо броя кликове на потребителя за определено време - Android Emulator 11 \(API 30\)_

