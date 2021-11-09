# Clicker Mania 1.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим универсално приложение отчитащо броя кликове на потребителя.

## Start

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект **Visual C\# &gt; Windows Universal &gt; Blank App \(Universal Windows\)**. 
3. За име на проекта запишете: **Clicker Mania 1.0**.

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

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

Изглед от дизайна на потребителският интерфейс \(XAML\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/34_Clicker_Mania_1.0_UI.png)

_Фиг. 34. Изглед от дизайна на потребителският интерфейс_

## MainPage.xaml.cs

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

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

Изглед от бизнес логиката \(C\#\) в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/35_Clicker_Mania_1.0_BL.png)

_Фиг. 35. Изглед от бизнес логиката на разработваното приложение_

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/36_Clicker_Mania_1.0_Run.png)

_Фиг.36. Универсалано приложение отчитащо броя кликове на потребителя._
