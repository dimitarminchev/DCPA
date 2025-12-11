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

От менюто **Project** &gt; **Manage NuGet Packages** потърсете и инсталирайте пакета **AngleSharp**, като е показано на фигурата:

![](/images/140_AngleSharp.png)

_Фиг. 40. Инсталация на допълнителен пакет към проекта_

Допълнителни пакети към проект можете да инсталитрате и алтернативно от менюто: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, като изпълните следната команда в конзолата:

```
PM> Install-Package AngleSharp -Version 0.16.1
```

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<!-- User Interface (UI): HTML Downloader 1.0 -->
<StackPanel Background="LightCoral" Padding="20">
        
        <!-- Title -->
        <TextBlock Text="HTML Downloader 1.0" FontSize="40" />

        <!-- URL -->
        <TextBlock Text="URL" FontSize="20" />
        <TextBox Name="URL" Text="http://www.minchev.eu" FontSize="20" />
        <Button Content="Download" Margin="0 10" Padding="20 10" FontSize="20" Click="Button_Click" />
        
        <!-- HTML -->
        <TextBox Name="HTML" Height="400" TextWrapping="Wrap" IsReadOnly="True" FontSize="20" />
    
</StackPanel>
```

Изглед от дизайна на потребителският интерфейс \(XAML\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/141_HTML_Downloader_1.0_UI.png)

_Фиг. 1.41. Изглед от дизайна на потребителският интерфейс_

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
// Business Logic (BL): HTML Downloader 1.0
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
            string html = await Download(new Uri(URL.Text));
            var temp = new HtmlParser().ParseDocument(html);
            string text = temp.Body.TextContent;
            HTML.Text = text;
        }

        // Download Handler
        private async Task<string> Download(Uri link)
        {
            HttpClient client = new HttpClient();
            return await client.GetStringAsync(link);
        }
}
```

## Demo

Изглед от бизнес логиката \(C\#\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/142_HTML_Downloader_1.0_BL.png)

_Фиг. 1.42. Изглед от бизнес логиката на разработваното приложение_

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/143_HTML_Downloader_1.0_Run.png)

_Фиг. 1.43 Универслано приложение за изтегляне HTML съдържанието на кода от Интернет страница_
