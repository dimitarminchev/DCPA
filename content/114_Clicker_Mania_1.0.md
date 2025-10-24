# Clicker Mania 1.0

Using the integrated development environment Visual Studio and the C\# programming language, we will develop a universal application that tracks the number of user clicks.

## Start

1. Launch the integrated development environment **Visual Studio**.
2. Create a new project **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. Name the project: **Clicker Mania 1.0**.

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the design of the user interface of the application being developed and is written in the XAML language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the program snippet provided below into your application.

```xml
<Page
    x:Class="Clicker_Mania_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Clicker_Mania_1._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Clicker Mania 1.0 -->
    <StackPanel Background="Orange" Padding="50">
        
        <!-- Title -->
        <TextBlock FontSize="40" 
                   HorizontalAlignment="Center" 
                   Text="Clicker Mania 1.0" />
       
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
</Page>
```

View of the user interface design \(XAML\) in the integrated development environment Visual Studio during the development of the application:

![](/images/34_Clicker_Mania_1.0_UI.png)

_Fig. 34. View of the user interface design_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code of the business logic of the application being developed and is written in the C\# programming language. Copy \(Ctrl+C\) and paste \(Ctrl+V\) the code snippet given below into your application.

```csharp
using System;
using System.IO;
using System.Text;
using Windows.Storage;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;

namespace Clicker_Mania_1._0
{
    /// <summary>
    /// Business Logic (BL): Clicker Mania 1.0
    /// </summary>
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
}
```

View of the business logic \(C\#\) in the integrated development environment Visual Studio during application development:

![](/images/35_Clicker_Mania_1.0_BL.png)

_Fig. 35. View of the business logic of the application being developed_

## Demo

Start the application from the menu: **Debug &gt; Start Debugging** or by pressing the **F5** key.

![](/images/36_Clicker_Mania_1.0_Run.png)

_Fig. 36. Universal application counting the number of user clicks_
