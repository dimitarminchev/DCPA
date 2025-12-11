# Clicker Mania 1.2

Using Visual Studio and C# we will build a Universal Windows Platform application that counts user clicks over a given period.

## Start

1. Launch **Visual Studio**.
2. Create a new project: **Visual C# > Windows Universal > Blank App (Universal Windows)**.
3. Name the project **Clicker Mania 1.2**.

## MainPage.xaml

The **MainPage.xaml** file contains the UI markup written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
<!-- User Interface (UI): Clicker Mania 1.2 -->
<StackPanel Background="Lime" Padding="30">
        
        <!-- Title -->
        <TextBlock FontSize="30" Padding="10" HorizontalAlignment="Center" Text="Clicker Mania 1.2" FontWeight="ExtraBlack" />

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
```

Design view (XAML) in Visual Studio while developing the application:

![](/images/137_Clicker_Mania_2.0_UI.png)

_Fig. 1.37. UI design view_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the business logic written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): Clicker Mania 1.2
public sealed partial class MainPage : Page
{
        // Dispatcher Timer
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
            // Clicks Per Minute
            CPM.Text = (float.Parse(Clicks.Text) / float.Parse(Timer.Text) * 60).ToString("N2");
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            int N = int.Parse(Clicks.Text);
            Clicks.Text = (++N).ToString();
        }
}
```

Business logic (C#) view in Visual Studio while developing the application:

![](/images/138_Clicker_Mania_2.0_BL.png)

_Fig. 1.38. Business logic view_

## Demo 

Start the app via **Debug > Start Debugging** or press **F5**.

![](/images/139_Clicker_Mania_2.0_Run.png)

_Fig. 1.39 Universal app that counts user clicks over a given period_

