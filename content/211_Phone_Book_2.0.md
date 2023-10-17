# Phone Book 2.0

Използвайки интегрираната среда за разработка Visual Studio и езика за програмиране C\# ще разработим мулти-платформено мобилно приложение за телефонен указател съдържащо списък с контакти. 

## Start 

1. Стартирайте интегрираната среда за разработка **Visual Studio**. 
2. Създайте нов проект: **Visual C\# &gt; Cross-Platform &gt; Mobile App \(Xamarin.Forms\)**. 
3. За име на проекта запишете: **Phone Book 2.0**.

Добавете допълнителни пакети към проекта като инсталирате: **NewtonSoft.Json** от менюто: **Tools &gt; NuGet Package Manager &gt; Package Manager Console**, като изпълните следните команди в конзолата:

```
PM> Install-Package Newtonsoft.Json -Version 13.0.1
```

## Contact.cs

Добавете нов клас **Contact.cs** съдържащ с;едният програмен фрагмент:

```csharp
using System;

namespace Phone_Book_2._0.Model
{
    public class Contact
    {
        private Uri picture;

        public Uri Picture
        {
            get { return picture; }
            set { picture = value; }
        }

        private string name;

        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        private string phone;

        public string Phone
        {
            get { return phone; }
            set { phone = value; }
        }

        public Contact(Uri picture, string name, string phone)
        {
            this.picture = picture;
            this.name = name;
            this.phone = phone;
        }
    }
}
```

## ViewModel.cs

Добавете нов клас **ViewModel.cs** съдържащ следният програмен фрагмент:

```csharp
using System;
using System.Collections;
using System.Collections.ObjectModel;
using Xamarin.Forms;

namespace Phone_Book_2._0.Model
{
    public static class ViewModel 
    {
        public static ObservableCollection<Contact> Contacts;

        static ViewModel()
        {
            Contacts = new ObservableCollection<Contact>();

            BindingBase.EnableCollectionSynchronization(Contacts, null, Callback);
        }

        private static void Callback(IEnumerable collection, object context, Action accessMethod, bool writeAccess)
        {
            lock (collection)
            {
                accessMethod?.Invoke();
            }
        }
    }
}
```

## MainPage.xaml

Файлът **MainPage.xaml** съдържа изходния код от дизайна на потребителския интерфейс на разработваното приложение и се пише на езика XAML. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Phone_Book_2._0.MainPage">

    <StackLayout Padding="50">

        <Label Text="Phone Book 2.0" FontSize="Large" FontAttributes="Bold" />

        <Button Text="Add" Clicked="Button_Clicked" />

        <ListView x:Name="ListView">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <ImageCell Text="{Binding Name}" 
                               Detail="{Binding Phone}" 
                               ImageSource="{Binding Picture}" />
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>

    </StackLayout>

</ContentPage>
```

## MainPage.xaml.cs 

Файлът **MainPage.xaml.cs** съдържа изходния код от бизнес логиката на разработваното приложение и се пише на програмният език C\#. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using Xamarin.Forms;
using Phone_Book_2._0.Model;

namespace Phone_Book_2._0
{
    public partial class MainPage : ContentPage
    {
        public MainPage(Contact contact = null)
        {
            InitializeComponent();

            this.ListView.ItemsSource = ViewModel.Contacts;

            if (contact is Contact)
            {
                ViewModel.Contacts.Add(contact);
            }
        }

        private async void Button_Clicked(object sender, System.EventArgs e)
        {
            await Navigation.PushModalAsync(new AddPage());
        }
    }
}
```

## AddPage.xaml

Добавете нова страница **AddPage.xaml**. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Phone_Book_2._0.AddPage">

    <StackLayout Padding="50">

        <Label Text="Add" FontSize="Large" FontAttributes="Bold" />

        <Label Text="Picture" FontSize="Large" />
        <Entry x:Name="Picture" FontSize="Large" />

        <Label Text="Name" FontSize="Large" />
        <Entry x:Name="Name" FontSize="Large" />

        <Label Text="Phone" FontSize="Large" />
        <Entry x:Name="Phone" FontSize="Large" />

        <Button Text="Save" Clicked="Button_Clicked" />

    </StackLayout>

</ContentPage>
```

## AppPage.xaml.cs 

Отворете файла **AddPage.xaml.cs**. Копирайте \(Ctrl+C\) и поставете \(Ctrl+V\) програмният фрагмент даден по-долу във Вашето приложение.

```csharp
using System;
using Xamarin.Forms;
using Phone_Book_2._0.Model;

namespace Phone_Book_2._0
{
    public partial class AddPage : ContentPage
    {
        public AddPage()
        {
            InitializeComponent();
        }

        private async void Button_Clicked(object sender, System.EventArgs e)
        {
            var contact = new Contact
            (
                picture: new Uri(this.Picture.Text),
                name: this.Name.Text,
                phone: this.Phone.Text
            );

            await Navigation.PushAsync(new MainPage(contact));
        }
    }
}
```

## Demo

Стартирайте приложението от менюто: **Debug &gt; Start Debugging** или като натиснете клавиш **F5**.

![](/images/64_Phone_Book_2.0.png)

_Фиг. 64. Демонстрация на работата на мулти-платформеното мобилно приложение за телефонен указател_

> #### Използвани изображения:
> 1. https://shorturl.at/aiN17
> 2. https://shorturl.at/kALP3
