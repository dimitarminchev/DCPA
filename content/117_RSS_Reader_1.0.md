# RSS Reader 1.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a universal application for reading Internet news feeds from RSS sources.

{% hint style='info' %}
#### Information
RSS is a software mechanism for exchanging news between two websites or between a website and a user. It represents a set of formats for feeding information from the World Wide Web.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/RSS)
{% endhint %}

## Start
1. Launch the integrated development environment **Visual Studio**.
2. Create a new project **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. Name the project: **RSS Reader 1.0**.

## Item.cs

Add a new class **Item.cs**, which will be used to store data for each news item from the feed.

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

The file **MainPage.xaml** contains the source code from the user interface design of the application being developed and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the program snippet given below into your application.

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

View of the user interface design \(XAML\) in the integrated development environment Visual Studio during the development of the application:

![](/images/44_RSS_Reader_1.0_UI.png)

_Fig. 44. View of the user interface design_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the business logic of the developed application and is written in the C\# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet provided below into your application.

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

View of the business logic \(C\#\) in the integrated development environment Visual Studio during application development:

![](/images/45_RSS_Reader_1.0_BL.png)

_Fig. 45. View of the business logic of the application under development_

Start the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/46_RSS_Reader_1.0_Run.png)

_Fig. 46. Universal application for reading Internet news feeds from RSS sources_
