# HTML Downloader 1.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a universal application to download the HTML content of code from a web page. 

{% hint style='info' %}
#### Information 
HTML is the main markup language for describing and designing web pages. HTML is a standard on the Internet, and the rules are defined by the international consortium W3C. 
- Source: [Wikipedia](https://en.wikipedia.org/wiki/HTML)
{% endhint %}

## Start 

1. Launch the integrated development environment **Visual Studio**. 
2. Create a new project **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. For the project name, enter: **HTML Downloader 1.0**. 

From the **Project** &gt; **Manage NuGet Packages**, search for and install the **AngleSharp** package, as shown in the figure: 

![](/images/40_AngleSharp.png)

_Fig. 40. Installation of an additional package for the project_

You can also install additional packages for a project alternatively from the menu: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, by executing the following command in the console:

```
PM> Install-Package AngleSharp -Version 0.16.1
```

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the user interface design of the application being developed and is written in XAML. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet provided below into your application.

```xml
<Page
    x:Class="HTML_Downloader_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:HTML_Downloader_1._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

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
</Page>

```

View of the user interface design \(XAML\) in the integrated development environment Visual Studio during the development of the application:

![](/images/41_HTML_Downloader_1.0_UI.png)

_Fig. 41. View of the user interface design_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the business logic of the developed application and is written in the C# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet provided below into your application.

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using AngleSharp.Html.Parser;

namespace HTML_Downloader_1._0
{
    /// <summary>
    /// Business Logic (BL): HTML Downloader 1.0
    /// </summary>
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
}
```

## Demo

A view of the business logic \(C\#\) in the integrated development environment Visual Studio during the application development:

![](/images/42_HTML_Downloader_1.0_BL.png)

_Fig. 42. View of the business logic of the application under development_

Run the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/43_HTML_Downloader_1.0_Run.png)

_Fig. 43. Universal application for downloading HTML content from a web page_
