# HTML Downloader 2.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим мулти-платформено мобилно приложение за изтегляне HTML съдържанието на кода от Интернет страница.

{% hint style='info' %}
#### Информация
HTML е основният маркиращ език за описание и дизайн на уеб страници. HTML е стандарт в Интернет, а правилата се определят от международния консорциум W3C.
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/HTML)
{% endhint %}

## Start 

1. Стартирайте интегрираната среда за разработка **Visual Studio**.
2. Създайте нов проект: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**.
3. За име на проекта запишете: **HTML Downloader 2.0**.

Инсталирайте допълнителен пакет към приложението от менюто: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, като изпълните следната команда в конзолата:

```
PM> Install-Package AngleSharp -Version 0.16.1
```

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="HTML_Downloader_2._0.MainPage">

    <!-- User Interface (UI): HTML Downloaders 2.0 -->
    <StackLayout Padding="20" BackgroundColor="LightCoral">

        <!-- Title -->
        <Label Text="HTML Downloader 2.0" FontSize="Large" />

        <!-- URL -->
        <Label Text="URL" FontSize="Large" />
        <Entry x:Name="URL" Text="https://www.minchev.eu" />
        <Button Text="Download" Clicked="OnButtonClicked" />

        <!-- HTML -->
        <ScrollView>
            <Label x:Name="HTML" />
        </ScrollView>

    </StackLayout>
</ContentPage>
```

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;
using Xamarin.Forms;
using AngleSharp.Html.Parser;

namespace HTML_Downloader_2._0
{
    /// <summary>
    /// Business Logic (BL): HTML Downloader 2.0
    /// </summary>
    public partial class MainPage : ContentPage
    {
        // Constructor
        public MainPage()
        {
            InitializeComponent();
        }

        // Button Click Event Handler
        private async void OnButtonClicked(object sender, EventArgs args)
        {
            // Get Html
            string html = await Download(new Uri(this.URL.Text));

            // Angle Sharp Html to Text Parser
            var temp = new HtmlParser().ParseDocument(html);
            string text = temp.Body.TextContent;

            // Plain Text
            this.HTML.Text = text;
        }

        // Download Handler
        private async Task<string> Download(Uri link)
        {
            HttpClient client = new HttpClient();
            return await client.GetStringAsync(link);
        }
    }
}
```

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/61_HTML_Downloader_2.0.png)

_Фиг.61 Тестване на мултиплатформено мобилно приложение за изтегляне HTML съдържанието на кода от Интернет страница - Android Emulator 11 \(API 30\)._

