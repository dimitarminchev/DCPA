# HTML Downloader 2.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a cross-platform mobile application to download the HTML content of code from a web page.

{% hint style='info' %}
#### Information
HTML is the primary markup language for describing and designing web pages. HTML is a standard on the Internet, and its rules are defined by the international consortium W3C.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/HTML)
{% endhint %}


## Start
1. Launch the integrated development environment **Visual Studio**.
2. Create a new project: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**.
3. Name the project: **HTML Downloader 2.0**.

Install an additional package into the application from the menu: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, by running the following command in the console:

```
PM> Install-Package AngleSharp -Version 0.16.1
```

## MainPage.xaml

The file **MainPage.xaml** contains the source code for the user interface design of the application being developed and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the program snippet given below into your application.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="HTML_Downloader_2._0.MainPage">

    <!-- User Interface (UI): HTML Downloaders 2.0 -->
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
</ContentPage>
```

## MainPage.xaml.cs

The file **MainPage.xaml.cs** contains the source code of the business logic of the developed application and is written in the C\# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;
using Xamarin.Forms;
using AngleSharp.Html.Parser;

namespace HTML_Downloader_2._0
{
    /// <summary>
    /// Business Logic (BL): HTML Downloader 2.0
    /// </summary>
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
            // Get Html
            string html = await Download(new Uri(this.URL.Text));

            // Angle Sharp Html to Text Parser
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
}
```

## Demo

Launch the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/61_HTML_Downloader_2.0.png)

_Fig.61 Testing a cross-platform mobile application for downloading HTML content from a webpage - Android Emulator 11 (API 30)._
