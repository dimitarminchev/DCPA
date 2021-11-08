# JSON Reader 1.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим универсално приложение за изтегляне на вицове за Чък Норис във формат [JSON](https://www.json.org/).

{% hint style='info' %}
#### Информация
JSON или JavaScript Object Notation, е текстово базиран отворен стандарт създаден за човешки четим обмен на данни. Произлиза от скриптовия език JavaScript, за да представя прости структури от данни и асоциативни масиви, наречени обекти.
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/JSON)
{% endhint %}

## Start

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект: **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. За име на проекта запишете: **JSON Reader 1.0**.

Добавете допълнителни пакети към проекта като инсталирате: **NewtownSoft.Json** и **AngleSharp**, от менюто: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, като изпълните следните команди в конзолата:

```
PM> Install-Package Newtonsoft.Json -Version 11.0.2
PM> Install-Package AngleSharp -Version 0.9.11
```

#### **RootObject.cs**

Добавете нов клас **RootObject.cs**, който ще служи за десериализиране на данните от консумираната услуга.

```csharp
namespace JSON_Reader_1._0
{
    // https://api.chucknorris.io/jokes/random
    // http://json2csharp.com/
    public class RootObject
    {
        public object category { get; set; }
        public string icon_url { get; set; }
        public string id { get; set; }
        public string url { get; set; }
        public string value { get; set; }
    }
}
```

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<Page
    x:Class="JSON_Reader_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): JSON Reader 1.0 -->
    <StackPanel Background="Pink" Padding="30">
        <TextBlock Text="JSON Reader 1.0"  FontSize="32" Margin="10"/>
        <TextBox Name="Joke" FontSize="23" TextWrapping="Wrap" Height="300" Margin="10" IsReadOnly="True" />
        <StackPanel Orientation="Horizontal">
            <Button Content="New joke" Width="120" FontSize="23" Padding="10" Margin="10" Click="Button_Get_Click"/>
            <Button Content="Tell joke" Width="120" FontSize="23" Padding="10" Margin="10" Click="Button_Tell_Click"/>
        </StackPanel>
    </StackPanel>

</Page>
```

Изглед от дизайна на потребителският интерфейс \(XAML\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/47.png)

_Фиг. 47. Изглед от дизайна на потребителският интерфейс_

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using System.Net.Http;
using Windows.Media.SpeechSynthesis;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Newtonsoft.Json;
using AngleSharp.Parser.Html;

namespace JSON_Reader_1._0
{
    // Business Logic (BL): JSON Reader 1.0
    public sealed partial class MainPage : Page
    {
        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
        }

        // Button Get Joke Event Handler
        private async void Button_Get_Click(object sender, RoutedEventArgs e)
        {
            // Download JSON
            HttpClient client = new HttpClient();
            var json = await client.GetStringAsync(new Uri("https://api.chucknorris.io/jokes/random"));

            // Deserialize the JSON
            var joke = JsonConvert.DeserializeObject<RootObject>(json);

            // Parse the HTML
            var html = new HtmlParser().Parse(joke.value);
            var text = html.Body.TextContent;

            // Tell the Joke
            Joke.Text = text;
        }

        // Button Tell Joke Event Handler
        private async void Button_Tell_Click(object sender, RoutedEventArgs e)
        {
            if (Joke.Text != "")
            {
                // The media object for controlling and playing audio.
                var mediaElement = new MediaElement();

                // The object for controlling the speech synthesis engine (voice).
                var synth = new SpeechSynthesizer();

                // Generate the audio stream from plain text.
                var stream = await synth.SynthesizeTextToStreamAsync(Joke.Text);

                // Send the stream to the media object.
                mediaElement.SetSource(stream, stream.ContentType);
                mediaElement.Play();
            }
        }
    }
}
```

## Demo

Изглед от бизнес логиката \(C\#\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/48.png)

_Фиг. 48. Изглед от бизнес логиката на разработваното приложение_

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.  

![](/images/49.png)

_Фиг.49 Универсално приложение за изтегляне на вицове за Чък Норис_
