# Clicker Mania 3.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a cross-platform mobile application that tracks the number of clicks by the user over a certain period of time.

## Start
1. Launch the integrated development environment **Visual Studio**.
2. Create a new project: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**. 
3. Name the project: **Clicker Mania 3.0**.

## MainPage.xaml

The file **MainPage.xaml** contains the source code for the design of the application's user interface and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code fragment provided below into your application.

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

The file **MainPage.xaml.cs** contains the source code of the business logic of the developed application and is written in the C\# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

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

Start the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/60_Clicker_Mania_3.0.png)

_Fig.60 Testing a cross-platform mobile application that counts the number of user clicks over a certain period - Android Emulator 11 (API 30)_
