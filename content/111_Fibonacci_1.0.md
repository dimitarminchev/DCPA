# Fibonacci 1.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a universal application for generating numbers from the Fibonacci sequence.

{% hint style='info' %}
#### Information
Fibonacci numbers in mathematics form a sequence that is defined recursively as follows: it starts with 0 and 1, and each subsequent member of the sequence is obtained as the sum of the previous two. The first Fibonacci numbers are: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, …
- Source: [Wikipedia](https://en.wikipedia.org/wiki/Fibonacci_number)
{% endhint %}

## Start

Launch the integrated development environment **Visual Studio**. Create a new project from the menu by following the sequence: **File &gt; New &gt; Project** or use the shortcut key combination **Ctrl + Shift + N**. In the dialog box that appears, select: **Visual C# > Windows Universal > Blank App (Universal Windows)**. For the project name, enter: **Fibonacci 1.0**. From the Solution Explorer, open the files **MainPage.xaml** and **MainPage.xaml.cs**. If you do not see the Solution Explorer, you can open it from the menu **View > Solution Explorer** or use the shortcut **Ctrl + W, S**. 

## MainPage.xaml

 The **MainPage.xaml** file contains the source code for the user interface design of the application being developed and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the following code snippet into your application.

```xml
<Page
    x:Class="Fibonacci_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Fibonacci_1._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Fibonacci 1.0 -->
    <StackPanel Background="Pink" Padding="50">
        
        <!-- Title -->
        <TextBlock Text="Fibonacci 1.0" FontSize="40" />

        <!-- Limit -->
        <TextBlock Text="Limit" Margin="0 10 0 10" FontSize="20" />
        <TextBox Name="boxLimit" FontSize="20" Text="1000" />
        <Button Content="Generate" Margin="0 10 0 10" Padding="20 10 20 10" FontSize="20"  Click="Button_Click" />
        
        <!-- Numbers -->
        <ListBox Name="boxNumbers"  Height="400" FontSize="20" />

    </StackPanel>
</Page>

```

View of the user interface design \(XAML\) in the integrated development environment Visual Studio during the application development:

![](/images/26_Fibonacci_1.0_UI.png)

_Fig. 26. View of the user interface design_

## MainPage.xaml.cs

The file **MainPage.xaml.cs** contains the source code for the business logic of the developed application and is written in the C# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

```csharp
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using System.Collections.ObjectModel;

namespace Fibonacci_1._0
{
    /// <summary>
    /// Business Logic (BL): Fibonacci 1.0
    /// </summary>
    public sealed partial class MainPage : Page
    {
        // Collection
        private ObservableCollection<int> numbers = new ObservableCollection<int>();

        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
            boxNumbers.ItemsSource = numbers;
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            numbers.Add(1);
            numbers.Add(1);
            int limit = int.Parse(boxLimit.Text);
            int a = 1, b = 1, c = a + b;
            while (c < limit)
            {
                numbers.Add(c);
                a = b;
                b = c;
                c = a + b;
            }
        }
    }
}
```

View of the business logic \(C\#\) in the integrated development environment Visual Studio during application development:

![](/images/27_Fibonacci_1.0_BL.png)

_Fig. 27. View of the business logic of the application under development._

## Demo

Run the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/28_Fibonacci_1.0_Run.png)

_Fig. 28. Universal application for generating Fibonacci sequence numbers._