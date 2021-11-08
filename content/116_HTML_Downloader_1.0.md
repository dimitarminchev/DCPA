# HTML Downloader 1.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим универсално приложение за изтегляне HTML съдържанието на кода от Интернет страница.

{% hint style='info' %}
#### Информация
HTML е основният маркиращ език за описание и дизайн на уеб страници. HTML е стандарт в Интернет, а правилата се определят от международния консорциум W3C.
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/HTML)
{% endhint %}

## Start

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. За име на проекта запишете: **HTML Downloader 1.0**.

От менюто **Project **&gt; **Manage NuGet Packages** потърсете и инсталирайте пакета **AngleSharp**, като е показано на фигурата:

![](/images/40.png)

_Фиг. 40. Инсталация на допълнителен пакет към проекта_

Допълнителни пакети към проект можете да инсталитрате и алтернативно от менюто: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, като изпълните следната команда в конзолата:

```
PM> Install-Package AngleSharp -Version 0.9.11
```

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<Page
    x:Class="HTML_Downloader_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): HTML Downloader 1.0 -->
    <StackPanel Background="Yellow" Padding="20">
        <TextBlock Text="HTML Downloader 1.0" FontSize="32" />
        <TextBlock Text="URL" />
        <TextBox Name="URL" Text="http://www.minchev.eu" />
        <Button Content="Download" Margin="0 10 0 10" Click="Button_Click" />
        <TextBox Name="HTML" Height="400" TextWrapping="Wrap" IsReadOnly="True" />
    </StackPanel>

</Page>
```

Изглед от дизайна на потребителският интерфейс \(XAML\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/41.png)

_Фиг. 41. Изглед от дизайна на потребителският интерфейс_

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using AngleSharp.Parser.Html;
using System;
using System.Net.Http;
using System.Threading.Tasks;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;

namespace HTML_Downloader_1._0
{
	/// <summary>
    /// Business Logic (BL): HTML Downloader 1.0
    /// </summary>
    public sealed partial class MainPage : Page
    {
        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
        }

        // Button Click Event Handler
        private async void Button_Click(object sender, RoutedEventArgs e)
        {
            string html = await Go(new Uri(URL.Text));
            var temp = new HtmlParser().Parse(html);
            string text = temp.Body.TextContent;
            HTML.Text = text;
        }

        // Get the HTML
        private async Task<string> Go(Uri link)
        {
            HttpClient client = new HttpClient();
            return await client.GetStringAsync(link);
        }
    }
}
```

## Demo

Изглед от бизнес логиката \(C\#\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/42.png)

_Фиг. 42. Изглед от бизнес логиката на разработваното приложение_

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/43.png)

_Фиг.43 Универслано приложение за изтегляне HTML съдържанието на кода от Интернет страница_