# Fibonacci 2.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим мулти-платформено мобилно приложение за генериране на числата от редицата на Фибоначи.

{% hint style='info' %}
#### Информация
Числата на Фибоначи в математиката образуват редица, която се дефинира рекурсивно по следния начин: започва се с 0 и 1, а всеки следващ член на редицата се получава като сума на предходните два. Първите числа на Фибоначи са: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, …
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/Fibonacci_number)
{% endhint %}

## Start
1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**. 
3. За име на проекта запишете: **Fibonacci 2.0**.

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение

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

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

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

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5.**

![](/images/58_Fibonacci_2.0.png)

_Фиг.58 Тестване на мултиплатформено мобилно приложение за генериране на редицата от числата на Фибоначи - Android Emulator 11 \(API 30\)_

