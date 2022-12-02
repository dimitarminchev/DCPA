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

Добавете допълнителни пакети към проекта като инсталирате: **NewtonSoft.Json** от менюто: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, като изпълните следните команди в конзолата:

```
PM> Install-Package Newtonsoft.Json -Version 13.0.1
```

## Root.cs

Добавете нов клас **Root.cs**, който ще служи за десериализиране на данните от консумираната услуга.

```csharp
using System.Collections.Generic;
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

    <!-- JSON Reader 2.0 User Interface -->
    <StackLayout Padding="50">

        <!-- Title -->
        <Label Text="JSON Reader 2.0" FontSize="Large" FontAttributes="Bold" />

        <!-- Buttons -->
        <StackLayout Orientation="Horizontal">
            <Button Text="New Joke" Clicked="NewJokeButtonClickedEventHandler" />
            <Button Text="Tell Joke" Clicked="TellJokeButtonClickedEventHandler" />
        </StackLayout>
        
        <!-- Joke -->
        <Label x:Name="JOKE" FontSize="Large" />

    </StackLayout>

</ContentPage>
```

## MainPage.xaml.cs 

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using System.Net.Http;
using Xamarin.Forms;
using Xamarin.Essentials;
using Newtonsoft.Json;

namespace JSON_Reader_2._0
{
    public partial class MainPage : ContentPage
    {
        /// <summary>
        /// Constructor
        /// </summary>
        public MainPage()
        {
            InitializeComponent(); 
        }

        /// <summary>
        /// New Joke Button Clicked Event Handler
        /// </summary>
        private async void NewJokeButtonClickedEventHandler(object sender, EventArgs e)
        {
            // 1. Http Client
            HttpClient client = new HttpClient();

            // 2. Http Request to Receive JSON Response
            string json = await client.GetStringAsync(new Uri("https://api.chucknorris.io/jokes/random"));

            // 3. Deserialize JSON to Object
            Joke joke = JsonConvert.DeserializeObject<Joke>(json);

            // 4. Show the Joke in the UI
            JOKE.Text = joke.value;
        }

        /// <summary>
        /// Tell Joke Button Clicked Event Handler
        /// </summary>
        private async void TellJokeButtonClickedEventHandler(object sender, EventArgs e)
        {
            var joke = JOKE.Text;
            if (joke != "")
            {
                await TextToSpeech.SpeakAsync(joke);
            }
        }
    }
}
```

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/63_JSON_Reader_2.0.png)

_Фиг. 63. Демонстрация на работата на мулти-платформеното мобилно приложение за изтегляне на вицове за Чък Норис_
