# JSON Reader 1.0

Using the integrated development environment Visual Studio and the programming language C\#, we will develop a universal application for downloading Chuck Norris jokes in [JSON](https://www.json.org/) format. 

{% hint style='info' %}
#### Information 
JSON or JavaScript Object Notation is a text-based open standard designed for human-readable data exchange. It originates from the JavaScript scripting language to represent simple data structures and associative arrays called objects. 
- Source: [Wikipedia](https://en.wikipedia.org/wiki/JSON)
{% endhint %}

## Start 

1. Launch the integrated development environment **Visual Studio**. 
2. Create a new project: **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. Name the project: **JSON Reader 1.0**. 

Add additional packages to the project by installing: **NewtonSoft.Json** and **AngleSharp**, from the menu: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, by executing the following commands in the console:

```
PM> Install-Package Newtonsoft.Json -Version 13.0.1
PM> Install-Package AngleSharp -Version 0.16.1
```

#### **Root.cs**

Add a new class **Root.cs**, which will be used for deserializing the data from the consumed service.

```csharp
namespace JSON_Reader_1._0
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

> #### Note
> 1. Load and copy sample JSON from: https://api.chucknorris.io/jokes/random
> 2. Generate the C# class of the selected JSON from: http://json2csharp.com/

## MainPage.xaml

The **MainPage.xaml** file contains the source code from the user interface design of the application being developed and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the program snippet given below into your application.

```xml
<Page
    x:Class="JSON_Reader_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:JSON_Reader_1._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): JSON Reader 1.0 -->
    <StackPanel Background="LightSalmon" Padding="30">
       
        <!-- Title -->
        <TextBlock Text="JSON Reader 1.0"  FontSize="40" Margin="10"/>
        
        <!-- Joke -->
        <TextBox Name="Joke" FontSize="20" TextWrapping="Wrap" Height="300" Margin="10" IsReadOnly="True" />
        
        <!-- Buttons -->
        <StackPanel Orientation="Horizontal">
            <Button Content="New joke" Width="120" FontSize="23" Padding="10" Margin="10" Click="Button_Get_Click"/>
            <Button Content="Tell joke" Width="120" FontSize="23" Padding="10" Margin="10" Click="Button_Tell_Click"/>
        </StackPanel>
        
    </StackPanel>
</Page>
```

View of the user interface design \(XAML\) in the integrated development environment Visual Studio during the development of the application:

![](/images/47_JSON_Reader_1.0_UI.png)

_Fig. 47. View of the user interface design_#

# MainPage.xaml.cs

The file **MainPage.xaml.cs** contains the source code for the business logic of the developed application and is written in the C\# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the program snippet given below into your application.

```csharp
using System;
using System.Net.Http;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using AngleSharp.Html.Parser;
using Newtonsoft.Json;
using Windows.Media.SpeechSynthesis;

namespace JSON_Reader_1._0
{
    /// <summary>
    /// Business Logic (BL): JSON Reader 1.0
    /// </summary>
    public sealed partial class MainPage : Page
    {
        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
        }

        // Button Get Joke Event Handler
        private async void Button_Get_Click(object sender, RoutedEventArgs e)
        {
            // Download JSON
            HttpClient client = new HttpClient();
            var json = await client.GetStringAsync(new Uri("https://api.chucknorris.io/jokes/random"));

            // Deserialize the JSON
            var joke = JsonConvert.DeserializeObject<Root>(json);

            // Parse the HTML
            var html = new HtmlParser().ParseDocument(joke.value);
            var text = html.Body.TextContent;

            // Tell the Joke
            Joke.Text = text;
        }

        // Button Tell Joke Event Handler
        private async void Button_Tell_Click(object sender, RoutedEventArgs e)
        {
            if (Joke.Text != "")
            {
                // The media object for controlling and playing audio.
                var mediaElement = new MediaElement();

                // The object for controlling the speech synthesis engine (voice).
                var synth = new SpeechSynthesizer();

                // Generate the audio stream from plain text.
                var stream = await synth.SynthesizeTextToStreamAsync(Joke.Text);

                // Send the stream to the media object.
                mediaElement.SetSource(stream, stream.ContentType);
                mediaElement.Play();
            }
        }
    }
}
```

View of the business logic \(C\#\) in the integrated development environment Visual Studio during application development:

![](/images/48_JSON_Reader_1.0_BL.png)

_Fig. 48. View of the business logic of the application under development_

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/49_JSON_Reader_1.0_Run.png)

_Fig. 49. Universal application for downloading Chuck Norris jokes_
