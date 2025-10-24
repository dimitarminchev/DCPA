# Primes 2.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a cross-platform mobile application to generate a sequence of prime numbers.

{% hint style='info' %}
#### Information
A prime number is a natural number greater than 1 that is not the product of two smaller natural numbers.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/Prime_number)
{% endhint %}

## Start
1. Launch the integrated development environment **Visual Studio**.
2. Create a new project: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**. 
3. For the project name, enter: **Primes 2.0**.

## MainPage.xaml

The file **MainPage.xaml** contains the source code for the design of the user interface of the application being developed and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the program snippet given below into your application. 

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим мулти-платформено мобилно приложение за генериране на редица от прости числа.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Primes_2._0.MainPage">

    <!-- User Interface (UI): Primes 2.0 -->
    <StackLayout Padding="20" BackgroundColor="Yellow">
        
        <!-- Title -->
        <Label Text="Primes 2.0" FontSize="Large" />

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

The file **MainPage.xaml.cs** contains the source code of the business logic of the developed application and is written in the programming language C\#. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

```csharp
using System;
using System.Collections.Generic;
using Xamarin.Forms;

namespace Primes_2._0
{
    /// <summary>
    /// Business Logic (BL): Primes 2.0
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
            List<int> primes = new List<int>();
            int limit = int.Parse(this.boxLimit.Text);
            for (int k = 2; k < limit; k++)
            {
                bool prime = true;
                for (int j = 2; j < k; j++) if (k % j == 0) prime = false;
                if (prime) primes.Add(k);
            }
            this.boxNumbers.ItemsSource = primes;
        }
    }
}
```

## Demo

Start the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/59_Primes_2.0.png)

_Fig.59 Testing a cross-platform mobile application for generating a sequence of prime numbers - Android Emulator 11 (API 30)_
