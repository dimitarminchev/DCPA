# RSS Reader 2.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a cross-platform mobile application for reading news feeds (RSS) from internet sources.

{% hint style='info' %}
#### Information
RSS is a software mechanism for exchanging news between websites or between a site and a user. It represents a set of formats for delivering information from the World Wide Web.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/RSS)
{% endhint %}

# Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project:  **Visual C# > Cross-Platform > Mobile App (Xamarin.Forms)**.
3. Name the project: **RSS Reader 2.0**.

## FeedReader.cs

Add a new class named `FeedReader.cs`, which will be used to store data from the news feed.

```csharp
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
            var feed = XDocument.Load(url);
            var posts = from item in feed.Descendants("item")
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
```

## HyperlinkButton.cs

Add a `HyperlinkButton.cs` class that will be used to add hyperlinks to the application's user interface, following Microsoft documentation: [Xamarin.Forms Hyperlinks Microsoft Docs](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/text/label#hyperlinks)

```cs
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
```

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
<!-- User Interface (UI): RSS Reader 2.0 -->
<StackLayout Padding="20" BackgroundColor="LightBlue">

        <!-- Title -->
        <Label Text="RSS Reader 2.0" FontSize="Large" />

        <!-- URI -->
        <Entry x:Name="URI" Text="https://www.minchev.eu/feed/" />
        <Button Text="Download" Clicked="Button_Clicked" />

        <!-- RSS -->
        <ListView x:Name="RSS">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <local:HyperlinkButton Text="{Binding Title}" Detail="{Binding PubDate}" Url="{Binding Link}" />
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
</StackLayout>
```

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): RSS Reader 2.0
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
            RSS.ItemsSource = new ObservableCollection<FeedItem>
            (
                new FeedReader().ReadFeed(URI.Text)
            );
        }
}
```

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/262_RSS_Reader_2.0.png)

_Fig. 2.62 Testing the cross-platform mobile application for reading internet news feeds (RSS sources) - Android Emulator 11 (API 30)._ 
