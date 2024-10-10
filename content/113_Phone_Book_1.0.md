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
        // Contacts
        public static ObservableCollection<Contact> contacts = new ObservableCollection<Contact>();

        ...
```

## AddPage.xaml

```xml
<Page
    x:Class="Phone_Book_1._0.AddPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Phone_Book_1._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Phone Book 1.0 -->
    <StackPanel Background="Cyan" Padding="40">

        <!-- Title -->
        <TextBlock Text="Add Contact" FontSize="40" />

        <!-- Name -->
        <TextBlock Text="Name" FontSize="20" />
        <TextBox Name="boxName" FontSize="20" />

        <!-- Phone -->
        <TextBlock Text="Phone" FontSize="20" />
        <TextBox Name="boxPhone" FontSize="20" />

        <!-- Picture -->
        <TextBlock Text="Picture" FontSize="20" />
        <TextBox Name="boxPicture" FontSize="20" />

        <!-- Button -->
        <Button Content="Add Contact" FontSize="20" Padding="20 10 20 10" Margin="0 20 0 0" Click="Button_Click" />
        
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
            var picture = new Uri(boxPicture.Text);
            var contact = new Contact(picture, boxName.Text, boxPhone.Text);
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
    xmlns:local="using:Phone_Book_1._0"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <!-- User Interface (UI): Phone Book 1.0 -->
    <StackPanel Background="Cyan" Padding="40">
        
        <!-- Title -->
        <TextBlock Text="Phone Book 1.0" FontSize="40" />
        
        <!-- Contacts -->
        <ListBox Name="boxContacts" Height="400">
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
        
        <!-- Add -->
        <Button Content="Add Contact"  FontSize="20" Padding="20 10 20 10" Margin="0 20 0 0" Click="Button_Click" />
        
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
            boxContacts.ItemsSource = App.contacts;
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            this.Frame.Navigate(typeof(AddPage));
        }

        // Navigation Event Handler
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Contact)
            {
                App.contacts.Add(e.Parameter as Contact);
            }
        }
    }
}
```

## Demo

Изглед в интегрираната среда за разработка Visual Studio по време на разработване на приложението:

![](/images/32_Phone_Book_1.0_Develop.png)

_Фиг. 32. Изглед от интегрираната среда за разработка по време на създаване на приложението_

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/33_Phone_Book_1.0_Run.png)

_Фиг. 33. Универсално приложение тип телефонен указател съдържащо списък с контакти_

> #### Използвани изображения за потребителски профили
> 1. Мъж: [https://icons-for-free.com/iconfiles/png/512/business+costume+male+man+office+user+icon-1320196264882354682.png](https://icons-for-free.com/business+costume+male+man+office+user+icon-1320196264882354682/)
> 2. Жена: [https://icons-for-free.com/iconfiles/png/512/female+person+user+woman+young+icon-1320196266256009072.png](https://icons-for-free.com/female+person+user+woman+young+icon-1320196266256009072/)
