# RSS Reader 1.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a universal application for reading news feeds (RSS) from internet sources.

{% hint style='info' %}
#### Information
RSS is a software mechanism for exchanging news between websites or between a site and a user. It represents a set of formats for delivering information from the World Wide Web.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/RSS)
{% endhint %}

## Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Windows Universal > Blank App (Universal Windows)**.
3. Name the project: **RSS Reader 1.0**.

## Item.cs

Add a new class `Item.cs` which will be used to store data for each news item in the feed.

```csharp
public class Item
{
    public string Title { get; set; }
    public string Link { get; set; }
    public string PublishedDate { get; set; }
}
```

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
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
```

View of the user interface design (XAML) in Visual Studio while developing the application:

![](/images/144_RSS_Reader_1.0_UI.png)

_Fig. 1.44. View of the user interface design_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): RSS Reader 1.0
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
```

## Demo

View of the business logic (C#) in Visual Studio while developing the application:

![](/images/145_RSS_Reader_1.0_BL.png)

_Fig. 1.45. View of the application's business logic_

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/146_RSS_Reader_1.0_Run.png)

_Fig. 1.46 Universal application for reading internet news feeds (RSS sources)_
