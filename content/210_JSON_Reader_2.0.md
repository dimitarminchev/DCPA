# JSON Reader 2.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим мулти-платформено мобилно приложение за изтегляне на вицове за Чък Норис във формат [JSON](https://www.json.org/).

{% hint style='info' %}
#### Информация
JSON или JavaScript Object Notation, е текстово базиран отворен стандарт създаден за човешки четим обмен на данни. Произлиза от скриптовия език JavaScript, за да представя прости структури от данни и асоциативни масиви, наречени обекти.
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/JSON)
{% endhint %}

## Start 

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**. 
3. За име на проекта запишете: **JSON Reader 2.0**.

Добавете допълнителни пакети към проекта като инсталирате: **NewtonSoft.Json** и **AngleSharp**, от менюто: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, като изпълните следните команди в конзолата:

```
PM> Install-Package Newtonsoft.Json -Version 13.0.1
PM> Install-Package AngleSharp -Version 0.16.1
```

## Root.cs

Добавете нов клас **Root.cs**, който ще служи за десериализиране на данните от консумираната услуга.

```csharp
namespace JSON_Reader_2._0
{
    public class Root
    {
        public List<object> categories { get; set; }
        public string created_at { get; set; }
        public string icon_url { get; set; }
        public string id { get; set; }
        public string updated_at { get; set; }
        public string url { get; set; }
        public string value { get; set; }
    }
}
```

> #### Бележка
> 1. Заредете и копирайте примерен JSON от: https://api.chucknorris.io/jokes/random
> 2. Генерирайте C# класа на избрания JSON от: http://json2csharp.com/

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="JSON_Reader_2._0.MainPage">

    <!-- User Interface (UI): JSON Reader 2.0 -->
    <StackLayout Padding="20" BackgroundColor="LightGray">
        
        <!-- Title -->
        <Label Text="JSON Reader 2.0" FontSize="Large" />
        
        <!-- Button -->
        <Button Text="Tell Me Joke" Clicked="OnButtonClicked" />
        
        <!-- Joke -->
        <ScrollView>
            <Label x:Name="Joke" />
        </ScrollView>
    </StackLayout>

</ContentPage>
```

## MainPage.xaml.cs 

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using System.Net.Http;
using Xamarin.Forms;
using AngleSharp.Html.Parser;
using Newtonsoft.Json;

namespace JSON_Reader_2._0
{
    /// <summary>
    /// Business Logic (BL): JSON Reader 2.0
    /// </summary>
    public partial class MainPage : ContentPage
    {
        // Constructor
        public MainPage()
        {
            InitializeComponent();
        }

        // Button Event Handler
        async void OnButtonClicked(object sender, EventArgs args)
        {
            // Download JSON
            HttpClient client = new HttpClient();
            var json = await client.GetStringAsync(new Uri("https://api.chucknorris.io/jokes/random"));

            // Deserialize the JSON
            var joke = JsonConvert.DeserializeObject<Root>(json);

            // Parse the HTML
            var html = new HtmlParser().ParseDocument(joke.value);
            var text = html.Body.TextContent;

            // Tell the Joke
            this.Joke.Text = text;
        }
    }
}
```

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/63_JSON_Reader_2.0.png)

_Фиг. 63. Демонстрация на работата на мулти-платформеното мобилно приложение за изтегляне на вицове за Чък Норис_
