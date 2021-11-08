# Phone Book 1.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим универсално приложение тип телефонен указател съдържащо списък с контакти. Изходния код от дизайна на потребителския интерфейс \(XAML\) и бизнес логиката \(C\#\) на приложението са дадени в програмните фрагменти по-долу:

## Contact.cs

```csharp
using System;
namespace Phone_Book_1._0
{
    public class Contact
    {
        public Uri picture { get; set; }
        public string name { get; set; }
        public string phone { get; set; }

        public Contact(Uri _picture, string _name, string _phone)
        {
            this.picture = _picture;
            this.name = _name;
            this.phone = _phone;
        }
    }
}
```

## App.xaml.cs

```csharp
using System;
using System.Collections.ObjectModel;
using Windows.ApplicationModel;
using Windows.ApplicationModel.Activation;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

namespace Phone_Book_1._0
{
    /// <summary>
    /// Provides application-specific behavior to supplement the default Application class.
    /// </summary>
    sealed partial class App : Application
    {
        // Phone Book 1.0
        public static ObservableCollection<Contact> people = new ObservableCollection<Contact>();

        ...
```

## AddPage.xaml

```xml
<Page
    x:Class="Phone_Book_1._0.AddPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Phone Book 1.0 -->
    <StackPanel Background="Pink" Padding="20">
        <TextBlock Text="Add Contact" FontSize="42" />
        <TextBlock Text="picture" FontSize="24" />
        <TextBox Name="picture" />
        <TextBlock Text="name" FontSize="24" />
        <TextBox Name="name" />
        <TextBlock Text="phone" FontSize="24" />
        <TextBox Name="phone" />
        <Button Content="Add" Click="Button_Click" />
    </StackPanel>

</Page>
```

## AddPage.xaml.cs

```csharp
using System;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;

namespace Phone_Book_1._0
{
    /// <summary>
    /// Business Logic (BL): Phone Book 1.0
    /// </summary>
    public sealed partial class AddPage : Page
    {
        // Constructor
        public AddPage()
        {
            this.InitializeComponent();
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            var contact = new Contact(new Uri(picture.Text), name.Text, phone.Text);
            this.Frame.Navigate(typeof(MainPage), contact);
        }
    }
}
```

## MainPage.xaml

```xml
<Page
    x:Class="Phone_Book_1._0.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Phone Book 1.0 -->
    <StackPanel Background="Pink" Padding="20">
        <TextBlock Text="PhoneBook 1.0" FontSize="42" />
        <ListBox Name="ListBoxPeople" Height="320">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <StackPanel Orientation="Horizontal">
                        <Image Source="{Binding picture}" Width="100" Height="100" />
                        <StackPanel>
                            <TextBlock Text="{Binding name}" FontSize="32" />
                            <TextBlock Text="{Binding phone}" FontSize="32" />
                        </StackPanel>
                    </StackPanel>
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
        <Button Content="Add Contact" Click="Button_Click" />
    </StackPanel>

</Page>
```

## MainPage.xaml.cs

```csharp
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

namespace Phone_Book_1._0
{
    /// <summary>
    /// Business Logic (BL): Phone Book 1.0
    /// </summary>
    public sealed partial class MainPage : Page
    {
        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
            ListBoxPeople.ItemsSource = App.people;
        }
		
        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            this.Frame.Navigate(typeof(AddPage));
        }
		
        // Navigate
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Contact)
                App.people.Add(e.Parameter as Contact);
        }
    }
}
```

## Demo

Изглед в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/32.png)

_Фиг. 32. Изглед от интегрираната среда за разработка по време на създаване на приложението_

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/33.png)

_Фиг. 33. Универсално приложение тип телефонен указател съдържащо списък с контакти_

