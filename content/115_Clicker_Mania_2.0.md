# Clicker Mania 2.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a universal application that tracks the number of clicks by the user over a certain period of time.

## Start

1. Launch the integrated development environment **Visual Studio**.
2. Create a new project **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. Name the project: **Clicker Mania 2.0**.

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the design of the user interface of the application being developed and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet provided below into your application.

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

View of the user interface design \(XAML\) in the integrated development environment Visual Studio during the development of the application:

![](/images/37_Clicker_Mania_2.0_UI.png)

_Fig. 37. View of the user interface design_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code of the business logic of the application being developed and is written in the C\# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

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

View of the business logic \(C\#\) in the integrated development environment Visual Studio during application development:

![](/images/38_Clicker_Mania_2.0_BL.png)

_Fig. 38. View of the business logic of the application being developed_

## Demo

Run the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/39_Clicker_Mania_2.0_Run.png)

_Fig. 39 Universal application counting user clicks over a certain period of time_
