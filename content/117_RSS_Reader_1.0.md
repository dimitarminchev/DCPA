# RSS Reader 1.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим универсално приложение за четене на Интернет новинарски емисии от RSS източници.

{% hint style='info' %}
#### Информация
RSS е софтуерен механизъм за обмен на новини между два сайта или между сайт и потребител. Представлява набор от формати за захранване с информация от световната Интернет мрежа.
- Източник: [Wikipedia](https://en.wikipedia.org/wiki/RSS)
{% endhint %}

## Start 

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. За име на проекта запишете: **RSS Reader 1.0**.

## Item.cs

Добавете нов клас **Item.cs**, който ще служи за съхранение на данни за всяка една новина от емисията.

```csharp
namespace RSS_Reader_1._0
{
    public class Item
    {
        public string Title { get; set; }
        public string Link { get; set; }
        public string PublishedDate { get; set; }
    }
}
```

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<Page
    x:Class="RSS_Reader_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:RSS_Reader_1._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): RSS Reader 1.0 -->
    <StackPanel Background="Lime" Padding="20">
        
        <!-- Title -->
        <TextBlock Text="RSS Reader 1.0" FontSize="40" />

        <!-- URI -->
        <TextBox Name="URI" Text="https://www.minchev.eu/feed/" FontSize="20" />
        <Button Content="Download" Margin="0 10" Padding="20 10" FontSize="20" Click="Button_Click" />

        <!-- RSS -->
        <ScrollViewer>
            <ListView Name="RSS">
                <ListView.ItemTemplate>
                    <DataTemplate>
                        <StackPanel>
                            <HyperlinkButton NavigateUri="{Binding Link}">
                                <HyperlinkButton.Content>
                                    <TextBlock TextWrapping="Wrap" Text="{Binding Title}"/>
                                </HyperlinkButton.Content>
                            </HyperlinkButton>
                            <TextBlock Text="{Binding PublishedDate}"/>
                        </StackPanel>
                    </DataTemplate>
                </ListView.ItemTemplate>
            </ListView>
        </ScrollViewer>
    </StackPanel>
</Page>
```

Изглед от дизайна на потребителският интерфейс \(XAML\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/44_RSS_Reader_1.0_UI.png)

_Фиг. 44. Изглед от дизайна на потребителският интерфейс_

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using System.Collections.ObjectModel;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.Web.Syndication;

namespace RSS_Reader_1._0
{
    /// <summary>
    /// Business Logic(BL): RSS Reader 1.0
    /// </summary>
    public sealed partial class MainPage : Page
    {
        // View Model
        private ObservableCollection<Item> Items = new ObservableCollection<Item>();

        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
            RSS.ItemsSource = Items;
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            Download();
        }

        // Download Handler
        private async void Download()
        {
            var uri = new Uri(URI.Text);
            var client = new SyndicationClient();
            var feed = await client.RetrieveFeedAsync(uri);
            if (feed != null)
            {
                foreach (var node in feed.Items)
                {
                    Items.Add(new Item
                    {
                        Title = node.Title.Text,
                        Link = node.Id,
                        PublishedDate = node.PublishedDate.ToString()
                    });
                }
            }
        }
    }
}
```

## Demo 

Изглед от бизнес логиката \(C\#\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/45_RSS_Reader_1.0_BL.png)

_Фиг. 45. Изглед от бизнес логиката на разработваното приложение_

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/46_RSS_Reader_1.0_Run.png)

_Фиг.46 Универсално приложение за четене на Интернет новинарски емисии от RSS източници_
