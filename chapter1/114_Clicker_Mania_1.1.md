# Clicker Mania 1.1

Using Visual Studio and C# we will build a Universal Windows Platform application that counts user clicks.

## Start

1. Launch **Visual Studio**.
2. Create a new project: **Visual C# > Windows Universal > Blank App (Universal Windows)**.
3. Name the project **Clicker Mania 1.1**.

## MainPage.xaml

The **MainPage.xaml** file contains the UI markup written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
<!-- User Interface (UI): Clicker Mania 1.1 -->
<StackPanel Background="Orange" Padding="50">
        
        <!-- Title -->
        <TextBlock FontSize="40" 
                   HorizontalAlignment="Center" 
                   Text="Clicker Mania 1.1" />
       
        <!-- Clicks -->
        <TextBlock Name="Clicks" 
                   HorizontalAlignment="Center" 
                   Text="0" FontSize="100" Padding="50" 
                   FontWeight="Black" />
        
        <!-- Button -->
        <Button Content="Click" 
                HorizontalAlignment="Center" 
                FontSize="40" 
                Padding="40 20 40 20"
                Click="Button_Click" />
        
</StackPanel>
```

Design view (XAML) in Visual Studio while developing the application:

![](/images/134_Clicker_Mania_1.0_UI.png)

_Fig. 1.34. UI design view_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the business logic written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): Clicker Mania 1.1
public sealed partial class MainPage : Page
{
        // Counter
        private int counter = 0;

        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
            Read();
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            counter = counter + 1;
            Clicks.Text = counter.ToString();
            Save(Clicks.Text);
        }

        // Save to File
        private async void Save(string content)
        {
            try
            {
                StorageFolder storage = ApplicationData.Current.LocalFolder;
                byte[] bytes = Encoding.UTF8.GetBytes(content.ToCharArray());
                var file = await storage.CreateFileAsync("clicker.txt", CreationCollisionOption.ReplaceExisting);
                using (var stream = await file.OpenStreamForWriteAsync())
                {
                    stream.Write(bytes, 0, bytes.Length);
                }
            }
            catch 
            {
              // On Error
            }
        }

        // Read from File
        private async void Read()
        {
            try
            {
                StorageFolder storage = ApplicationData.Current.LocalFolder;
                StorageFile file = await storage.GetFileAsync("clicker.txt");
                if (file == null)
                {
                    file = await storage.CreateFileAsync("clicker.txt");
                }
                else
                {
                    Stream stream = await file.OpenStreamForReadAsync();
                    StreamReader reader = new StreamReader(stream);
                    Clicks.Text = reader.ReadToEnd();
                    if (Clicks.Text == "")
                    {
                        Clicks.Text = "0";
                        counter = 0;
                    }
                    else counter = int.Parse(Clicks.Text);
                }
            }
            catch 
            {
                // On Error
            }
        }
}
```

Business logic (C#) view in Visual Studio while developing the application:

![](/images/135_Clicker_Mania_1.0_BL.png)

_Fig. 1.35. Business logic view_

## Demo

Start the app via **Debug > Start Debugging** or press **F5**.

![](/images/136_Clicker_Mania_1.0_Run.png)

_Fig. 1.36. Universal app that counts user clicks._
