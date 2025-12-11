# Phone Book 2.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a cross-platform mobile application for a phone book containing a list of contacts.

## Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Cross-Platform > Mobile App (Xamarin.Forms)**.
3. Name the project: **Phone Book 2.0**.

Add additional packages to the project by installing `Newtonsoft.Json` from: **Tools > NuGet Package Manager > Package Manager Console**, by running the following command in the console:

```
PM> Install-Package Newtonsoft.Json -Version 13.0.1
```

## Contact.cs

Add a new class `Contact.cs` containing the following code fragment:

```csharp
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
```

## ViewModel.cs

Add a new class `ViewModel.cs` containing the following code fragment:

```csharp
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
```

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
<!-- User Interface (UI): Phone Book 2.0 -->
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
```

## MainPage.xaml.cs 

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): Phone Book 2.0
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

        private void Button_Clicked(object sender, System.EventArgs e)
        {
             Navigation.PushModalAsync(new AddPage());
        }
}
```

## AddPage.xaml

Add a new page `AddPage.xaml`. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
<!-- User Interface (UI): Phone Book 2.0 -->
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
```

## AddPage.xaml.cs 

Open the file **AddPage.xaml.cs**. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): Phone Book 2.0
public partial class AddPage : ContentPage
{
        public AddPage()
        {
            InitializeComponent();
        }

        private void Button_Clicked(object sender, System.EventArgs e)
        {
            var contact = new Contact
            (
                picture: new Uri(this.Picture.Text),
                name: this.Name.Text,
                phone: this.Phone.Text
            );

            Navigation.PushModalAsync(new MainPage(contact));
        }
}
```

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/264_Phone_Book_2.0.png)

_Fig. 2.64. Demonstration of the cross-platform mobile phone book application_

> ### Used images for user profiles
> 1. Male: https://icons-for-free.com/business+costume+male+man+office+user+icon-1320196264882354682.png
> 2. Female: https://icons-for-free.com/female+person+user+woman+young+icon-1320196266256009072.png
