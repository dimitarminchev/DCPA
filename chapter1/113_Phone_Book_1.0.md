# Phone Book 1.0

Using Visual Studio and C# we will build a Universal Windows Platform phone book application that displays a list of contacts. The UI (XAML) and business logic (C#) code snippets are shown below.

## Contact.cs

```csharp
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
```

## App.xaml.cs

```csharp
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
```

## AddPage.xaml.cs

```csharp
// Business Logic (BL): Phone Book 1.0
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
```

## MainPage.xaml

```xml
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
```

## MainPage.xaml.cs

```csharp
// Business Logic (BL): Phone Book 1.0
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
```

## Demo

Design view in Visual Studio while developing the application:

![](/images/132_Phone_Book_1.0_Develop.png)

_Fig. 1.32. Visual Studio view during app development_

Start the app via **Debug > Start Debugging** or press **F5**.

![](/images/133_Phone_Book_1.0_Run.png)

_Fig. 1.33. Universal phone book app showing a list of contacts_

> #### Profile images used
> 1. Male: [https://icons-for-free.com/iconfiles/png/512/business+costume+male+man+office+user+icon-1320196264882354682.png](https://icons-for-free.com/business+costume+male+man+office+user+icon-1320196264882354682/)
> 2. Female: [https://icons-for-free.com/iconfiles/png/512/female+person+user+woman+young+icon-1320196266256009072.png](https://icons-for-free.com/female+person+user+woman+young+icon-1320196266256009072/)
