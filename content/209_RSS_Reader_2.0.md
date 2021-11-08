# RSS Reader 2.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим мулти-платформено мобилно приложение за четене на Интернет новинарски емисии от RSS източници.

{% hint style='info' %}
#### Информация
RSS е софтуерен механизъм за обмен на новини между два сайта или между сайт и потребител. Представлява набор от формати за захранване с информация от световната Интернет мрежа.
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/RSS)
{% endhint %}

# Start

1. Стартирайте интегрираната среда за разработка **Visual Studio**.
2. Създайте нов проект:  **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**.
3. За име на проекта запишете: **RSS Reader 2.0**.

## FeedReader.cs

Добавете нов клас наречен **FeedReader.cs**, който ще служи за съхранение на данни от новинарската емисия.

```csharp
using System.Linq;
using System.Xml.Linq;
using System.Collections.Generic;

namespace RSS_Reader_2._0
{
    /// <summary>
    /// RSS Feed Item
    /// </summary>
    public class FeedItem
    {
        public string Title { get; set; }
        public string Description { get; set; }
        public string Link { get; set; }
        public string PubDate { get; set; }
    }

    /// <summary>
    /// RSS Feed Reader
    /// </summary>
    public class FeedReader
    {
        public IEnumerable<FeedItem> ReadFeed(string url)
        {
            var rssFeed = XDocument.Load(url);
            var posts = from item in rssFeed.Descendants("item")
                        select new FeedItem
                        {
                            Title = item.Element("title").Value,
                            Description = item.Element("description").Value,
                            Link = item.Element("link").Value,
                            PubDate = item.Element("pubDate").Value
                        };
            return posts;
        }
    }
}
```

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="RSS_Reader_2._0.MainPage">

    <!-- User Interface (UI): RSS Reader 2.0 -->
    <StackLayout Padding="20">
        <Label Text="RSS Reader 2.0" FontSize="Large" />
        <Entry x:Name="EntryURL" Text="https://www.minchev.eu/feed/" />
        <Button Text="Download" Clicked="Button_Clicked" />
        <ListView x:Name="ListViewRSS">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <TextCell Text="{Binding Title}" Detail="{Binding PubDate}" />
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    </StackLayout>

</ContentPage>
```

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using System.Collections.ObjectModel;
using Xamarin.Forms;

namespace RSS_Reader_2._0
{
    /// <summary>
    /// Business Loginc (BL): RSS Reader 2.0
    /// </summary>
    public partial class MainPage : ContentPage
    {
        // Constructor
        public MainPage()
        {
            InitializeComponent();
        }

        // Button Click Event Handler
        private void Button_Clicked(object sender, EventArgs e)
        {
            var link = this.EntryURL.Text;
            var posts = new FeedReader().ReadFeed(link);
            this.ListViewRSS.ItemsSource = new ObservableCollection<FeedItem>(posts);
        }
    }
}
```

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/67.png)

_Фиг.67 Разработка на мултиплатформено мобилно приложение за четене на Интернет новинарски емисии от RSS източници._

![](/images/68.png)

_Фиг.68 Тестване на на мултиплатформено мобилно приложение за четене на Интернет новинарски емисии от RSS източници- Android Emulator 7.1 \(API 25\)._

# Hyperlinks

Актуализация за добавяне на хипер-връзки по документацията: [Xamarin.Forms Hyperlinks Microsoft Docs](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/text/label#hyperlinks)

## HyperlinkButton.cs

```cs
using Xamarin.Forms;
using Xamarin.Essentials;

namespace RSS_Reader_2._0
{
    /// <summary>
    /// Hyperlink Button Control
    /// </summary>
    public class HyperlinkButton : TextCell
    {
        // Url Property
        public static readonly BindableProperty UrlProperty = BindableProperty.Create(
                               nameof(Url), typeof(string), typeof(HyperlinkButton), null);
        public string Url
        {
            get { return (string)GetValue(UrlProperty); }
            set { SetValue(UrlProperty, value); }
        }

        // Constructor
        public HyperlinkButton()
        {
            Tapped += HyperlinkButton_Tapped;
        }

        // Tapped Event Handler
        private void HyperlinkButton_Tapped(object sender, System.EventArgs e)
        {
            // Launcher.OpenAsync is provided by Xamarin.Essentials.
            Command = new Command(async () => await Launcher.OpenAsync(Url));
        }
    }
}
```

## MainPage.xaml.cs

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:RSS_Reader_2._0"
             x:Class="RSS_Reader_2._0.MainPage">

    <!-- User Interface (UI): RSS Reader 2.0 -->
    <StackLayout Padding="20">
        <Label Text="RSS Reader 2.0" FontSize="Large" />
        <Entry x:Name="EntryURL" Text="https://www.minchev.eu/feed/" />
        <Button Text="Download" Clicked="Button_Clicked" />
        <ListView x:Name="ListViewRSS">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <local:HyperlinkButton Text="{Binding Title}" 
                                           Detail="{Binding PubDate}"
                                           Url="{Binding Link}" />
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    </StackLayout>
</ContentPage>
```