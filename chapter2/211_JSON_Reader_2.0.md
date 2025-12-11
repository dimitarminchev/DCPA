# JSON Reader 2.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a cross-platform mobile application for downloading Chuck Norris jokes in [JSON](https://www.json.org/) format.

{% hint style='info' %}
#### Information
JSON (JavaScript Object Notation) is a text-based open standard designed for human-readable data interchange. It originates from the JavaScript scripting language to represent simple data structures and associative arrays called objects.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/JSON)
{% endhint %}

## Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Cross-Platform > Mobile App (Xamarin.Forms)**.
3. Name the project: **JSON Reader 2.0**.

Add additional packages to the project by installing `Newtonsoft.Json` from: **Tools > NuGet Package Manager > Package Manager Console**, by running the following command in the console:

```
PM> Install-Package Newtonsoft.Json -Version 13.0.1
```

## Root.cs

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
<!-- User Interface (UI): JSON Reader 2.0 -->
<StackLayout Padding="50">

        <!-- Title -->
        <Label Text="JSON Reader 2.0" FontSize="Large" FontAttributes="Bold" />

        <!-- Buttons -->
        <StackLayout Orientation="Horizontal">
            <Button Text="New Joke" Clicked="NewJokeButtonClickedEventHandler" />
            <Button Text="Tell Joke" Clicked="TellJokeButtonClickedEventHandler" />
        </StackLayout>
        
        <!-- Joke -->
        <Label x:Name="JOKE" FontSize="Large" />

</StackLayout>
```

## MainPage.xaml.cs 

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): JSON Reader 2.0
public partial class MainPage : ContentPage
{
        /// <summary>
        /// Constructor
        /// </summary>
        public MainPage()
        {
            InitializeComponent(); 
        }

        /// <summary>
        /// New Joke Button Clicked Event Handler
        /// </summary>
        private async void NewJokeButtonClickedEventHandler(object sender, EventArgs e)
        {
            // 1. Http Client
            HttpClient client = new HttpClient();

            // 2. Http Request to Receive JSON Response
            string json = await client.GetStringAsync(new Uri("https://api.chucknorris.io/jokes/random"));

            // 3. Deserialize JSON to Object
            Joke joke = JsonConvert.DeserializeObject<Joke>(json);

            // 4. Show the Joke in the UI
            JOKE.Text = joke.value;
        }

        /// <summary>
        /// Tell Joke Button Clicked Event Handler
        /// </summary>
        private async void TellJokeButtonClickedEventHandler(object sender, EventArgs e)
        {
            var joke = JOKE.Text;
            if (joke != "")
            {
                await TextToSpeech.SpeakAsync(joke);
            }
        }
}
```

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/263_JSON_Reader_2.0.png)

_Fig. 2.63. Demonstration of the cross-platform mobile application for downloading Chuck Norris jokes_
