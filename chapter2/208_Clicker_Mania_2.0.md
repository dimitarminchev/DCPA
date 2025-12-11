# Clicker Mania 3.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a cross-platform mobile application that counts the user's clicks during a given time.

## Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Cross-Platform > Mobile App (Xamarin.Forms)**.
3. Name the project: **Clicker Mania 3.0**.

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application

```xml
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
```

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
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
            // Clicks Per Minute
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
```

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/260_Clicker_Mania_3.0.png)

_Fig. 2.60 Testing the cross-platform mobile application that counts user clicks during a given time - Android Emulator 11 (API 30)_

