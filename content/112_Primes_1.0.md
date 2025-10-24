# Primes 1.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a universal application for generating a sequence of prime numbers.

{% hint style='info' %}
#### Information
A prime number is a natural number greater than 1 that is not the product of two smaller natural numbers.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/Prime_number)
{% endhint %}

## Start

1. Launch the integrated development environment **Visual Studio**.
2. Create a new project **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. Name the project: **Primes 1.0**.

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the design of the application's user interface and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the program snippet provided below into your application.

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

View of the user interface design \(XAML\) in the integrated development environment Visual Studio during the application development:

![](/images/29_Primes_1.0_UI.png)

_Fig. 29. View of the user interface design_

## MainPage.xaml.cs

The file **MainPage.xaml.cs** contains the source code for the business logic of the developed application and is written in the C\# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

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

View of the business logic \(C\#\) in the integrated development environment Visual Studio during the application development:

![](/images/30_Primes_1.0_BL.png)

_Fig. 30. View of the business logic of the developed application_

## Demo

Run the application from the menu: **Debug &gt; Start Debugging** or by pressing **F5**.

![](/images/31_Primes_1.0_Run.png)

_Fig. 31. Universal application for generating a sequence of prime numbers._
