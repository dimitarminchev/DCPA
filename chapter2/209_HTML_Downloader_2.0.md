# HTML Downloader 2.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a cross-platform mobile application to download the HTML content of a web page.

{% hint style='info' %}
#### Information
HTML is the standard markup language for describing and designing web pages. HTML is a standard on the Internet and its rules are defined by the World Wide Web Consortium (W3C).
- Source: [Wikipedia](https://en.wikipedia.org/wiki/HTML)
{% endhint %}

## Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Cross-Platform > Mobile App (Xamarin.Forms)**.
3. Name the project: **HTML Downloader 2.0**.

Install the additional package for the app from: **Tools > NuGet Package Manager > Package Manager Console**, by running the following command in the console:

```
PM> Install-Package AngleSharp -Version 0.16.1
```

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
<!-- User Interface (UI): HTML Downloader 2.0 -->
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
```

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): HTML Downloader 2.0
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
            // Get HTML
            string html = await Download(new Uri(this.URL.Text));

            // AngleSharp HTML to Text Parser
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
```

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/261_HTML_Downloader_2.0.png)

_Fig. 2.61 Testing the cross-platform mobile application for downloading the HTML content of a web page - Android Emulator 11 (API 30)._ 

