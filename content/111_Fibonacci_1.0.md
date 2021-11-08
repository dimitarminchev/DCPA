# Fibonacci 1.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим универсално приложение загенериране на числата от редицата на Фибоначи.

{% hint style='info' %}
#### Информация
Числата на Фибоначи в математиката образуват редица, която се дефинира рекурсивно по следния начин: започва се с 0 и 1, а всеки следващ член на редицата се получава като сума на предходните два. Първите числа на Фибоначи са: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, …
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/Fibonacci_number)
{% endhint %}

## Start

Стартирайте интегрираната среда за разработка **Visual Studio**. Създайте нов проект от менюто посредством изпълняване на последователността: **File &gt; New &gt; Project** или използвайте съкратената клавишна комбинация **Ctrl + Shift + N**. В появилия се диалогов прозорец изберете: **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. За име на проекта запишете: **Fibonacci 1.0**. От Solution Explorer отворете файловете **MainPage.xaml** и **MainPage.xaml.cs**. В случай, че не виждате Solution Explorer можете да го отворите от менюто **View &gt; Solution Explorer** или като използвате съкратената клавишна последователност **Ctrl + W, S**.



## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<Page
    x:Class="Fibonacci_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Fibonacci 1.0 -->
    <StackPanel Background="Pink" Padding="50">
        <TextBlock Text="Фибоначи 1.0" FontSize="32" />
        <TextBlock Text="Ограничение" FontSize="23" />
        <TextBox Name="TextBoxLimit" Text="1000" />
        <ListBox Name="ListBoxFib" Height="320" FontSize="23" />
        <Button Content="Генерирай" FontSize="23" Click="Button_Click" />
    </StackPanel>

</Page>
```

Изглед от дизайна на потребителският интерфейс \(XAML\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/26.png)

_Фиг. 26. Изглед от дизайна на потребителският интерфейс_



## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System.Collections.ObjectModel;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;

namespace Fibonacci_1._0
{
    // Business Logic (BL): Fibonacci 1.0
    public sealed partial class MainPage : Page
    {
        // Collection
        private ObservableCollection<int> fib = new ObservableCollection<int>();

        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
            ListBoxFib.ItemsSource = fib;
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            fib.Add(1);
            fib.Add(1);
            int limit = int.Parse(TextBoxLimit.Text);
            int a = 1, b = 1, c = a + b;
            while (c < limit)
            {
                fib.Add(c);
                a = b;
                b = c;
                c = a + b;
            }
        }
    }
}
```

Изглед от бизнес логиката \(C\#\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/27.png)

_Фиг. 27. Изглед от бизнес логиката на разработваното приложение_

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/28.png)

_Фиг. 28. Универсално приложение за генериране на числата от редицата на Фибоначи._
