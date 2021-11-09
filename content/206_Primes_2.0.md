# Primes 2.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим мулти-платформено мобилно приложение за генериране на редица от прости числа.

{% hint style='info' %}
#### Информация
Просто число е естествено число, по-голямо от 1, което не е произведение на две по-малки естествени числа.
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/Prime_number)
{% endhint %}

## Start

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**. 
3. За име на проекта запишете: **Primes 2.0**.

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение

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

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

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

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/59_Primes_2.0.png)

_Фиг.59 Тестване на мултиплатформено мобилно приложение за генериране на редица от прости числа - Android Emulator 11 \(API 30\)_

