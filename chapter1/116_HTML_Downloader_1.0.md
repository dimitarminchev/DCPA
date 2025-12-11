# HTML Downloader 1.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a universal application to download the HTML content of a web page.

{% hint style='info' %}
#### Information
HTML is the standard markup language for describing and designing web pages. HTML is a standard on the Internet and its rules are defined by the World Wide Web Consortium (W3C).
- Source: [Wikipedia](https://en.wikipedia.org/wiki/HTML)
{% endhint %}

## Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Windows Universal > Blank App (Universal Windows)**.
3. Name the project: **HTML Downloader 1.0**.

From the **Project** > **Manage NuGet Packages** menu, search for and install the **AngleSharp** package, as shown in the figure:

![](/images/140_AngleSharp.png)

_Fig. 40. Installing an additional package to the project_

You can also install additional packages for the project alternatively from: **Tools > NuGet Package Manager > Package Manager Console**, by running the following command in the console:

```
PM> Install-Package AngleSharp -Version 0.16.1
```

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the program fragment below into your application.

```xml
<!-- User Interface (UI): HTML Downloader 1.0 -->
<StackPanel Background="LightCoral" Padding="20">
        
        <!-- Title -->
        <TextBlock Text="HTML Downloader 1.0" FontSize="40" />

        <!-- URL -->
        <TextBlock Text="URL" FontSize="20" />
        <TextBox Name="URL" Text="http://www.minchev.eu" FontSize="20" />
        <Button Content="Download" Margin="0 10" Padding="20 10" FontSize="20" Click="Button_Click" />
        
        <!-- HTML -->
        <TextBox Name="HTML" Height="400" TextWrapping="Wrap" IsReadOnly="True" FontSize="20" />
    
</StackPanel>
```

View of the user interface design (XAML) in Visual Studio while developing the application:

![](/images/141_HTML_Downloader_1.0_UI.png)

_Fig. 1.41. View of the user interface design_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the program fragment below into your application.

```csharp
// Business Logic (BL): HTML Downloader 1.0
public sealed partial class MainPage : Page
{
        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
        }

        // Button Click Event Handler
        private async void Button_Click(object sender, RoutedEventArgs e)
        {
            string html = await Download(new Uri(URL.Text));
            var temp = new HtmlParser().ParseDocument(html);
            string text = temp.Body.TextContent;
            HTML.Text = text;
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

View of the business logic (C#) in Visual Studio while developing the application:

![](/images/142_HTML_Downloader_1.0_BL.png)

_Fig. 1.42. View of the application's business logic_

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/143_HTML_Downloader_1.0_Run.png)

_Fig. 1.43 Universal application for downloading the HTML content of a web page_
