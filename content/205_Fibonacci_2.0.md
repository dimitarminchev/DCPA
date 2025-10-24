# Fibonacci 2.0

Using the integrated development environment Visual Studio and the Cю# programming language, we will develop a cross-platform mobile application for generating numbers from the Fibonacci sequence.

{% hint style='info' %}
#### Information
In mathematics, Fibonacci numbers form a sequence that is defined recursively as follows: it starts with 0 and 1, and each subsequent number in the sequence is obtained as the sum of the previous two. The first Fibonacci numbers are: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, …
- Source: [Wikipedia](https://en.wikipedia.org/wiki/Fibonacci_number)
{% endhint %}

## Start
1. Launch the integrated development environment **Visual Studio**.
2. Create a new project: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**.
3. Name the project: **Fibonacci 2.0**.

## MainPage.xaml

The file **MainPage.xaml** contains the source code for the user interface design of the application being developed and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Fibonacci_2._0.MainPage">

    <!-- User Interface (UI): Fibonacci 2.0 -->
    <StackLayout Padding="20">
        
        <!-- Title -->
        <Label Text="Fibonacci 2.0" FontSize="Large" />
        
        <!-- Limit -->
        <Label Text="Limit" />
        <Entry x:Name="boxLimit" Keyboard="Numeric" Text="1000" />
        <Button Text="Generate" Clicked="OnButtonClicked" />
        
        <!-- Numbers -->
        <ListView x:Name="boxNumbers" />
        
    </StackLayout>
</ContentPage>
```

## MainPage.xaml.cs

The file **MainPage.xaml.cs** contains the source code of the business logic of the developed application and is written in the C\# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

```csharp
using System;
using System.Collections.Generic;
using Xamarin.Forms;

namespace Fibonacci_2._0
{
    /// <summary>
    /// Business Logic (BL): Fibonacci 2.0
    /// </summary>
    public partial class MainPage : ContentPage
    {
        // Constructor
        public MainPage()
        {
            InitializeComponent();
        }

        // Button Click Event Handler
        void OnButtonClicked(object sender, EventArgs args)
        {
            List<int> numbers = new List<int>();
            numbers.Add(1);
            numbers.Add(1);
            int limit = int.Parse(this.boxLimit.Text);
            int a = 1, b = 1, c = a + b;
            while (c < limit)
            {
                numbers.Add(c);
                a = b;
                b = c;
                c = a + b;
            }
            this.boxNumbers.ItemsSource = numbers;
        }
    }
}
```

## Demo

Start the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/58_Fibonacci_2.0.png)

_Fig.58 Testing a cross-platform mobile application for generating the Fibonacci sequence - Android Emulator 11 (API 30)_
