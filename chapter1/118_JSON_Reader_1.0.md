# JSON Reader 1.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a universal application for downloading Chuck Norris jokes in [JSON](https://www.json.org/) format.

{% hint style='info' %}
#### Information
JSON (JavaScript Object Notation) is a text-based open standard designed for human-readable data interchange. It originates from the JavaScript scripting language to represent simple data structures and associative arrays called objects.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/JSON)
{% endhint %}

## Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Windows Universal > Blank App (Universal Windows)**.
3. Name the project: **JSON Reader 1.0**.

Add additional packages to the project by installing `Newtonsoft.Json` and `AngleSharp` from: **Tools > NuGet Package Manager > Package Manager Console**, running the following commands in the console:

```
PM> Install-Package Newtonsoft.Json -Version 13.0.1
PM> Install-Package AngleSharp -Version 0.16.1
```

#### `Root.cs`

Add a new class `Root.cs` that will be used to deserialize the data returned by the service.

```csharp
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
```

> #### Note
> 1. Load and copy an example JSON from: https://api.chucknorris.io/jokes/random
> 2. Generate the C# class for the selected JSON from: http://json2csharp.com/

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
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
```

View of the user interface design (XAML) in Visual Studio while developing the application:

![](/images/147_JSON_Reader_1.0_UI.png)

_Fig. 1.47. View of the user interface design_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): JSON Reader 1.0
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
```

View of the business logic (C#) in Visual Studio while developing the application:

![](/images/148_JSON_Reader_1.0_BL.png)

_Fig. 1.48. View of the application's business logic_

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.  

![](/images/149_JSON_Reader_1.0_Run.png)

_Fig. 1.49 Universal application for downloading Chuck Norris jokes_
