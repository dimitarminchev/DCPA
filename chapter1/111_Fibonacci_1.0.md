# Fibonacci 1.0

Using Visual Studio and C# we will build a Universal Windows Platform application that generates numbers from the Fibonacci sequence.

{% hint style='info' %}
#### Info
In mathematics, the Fibonacci numbers form a sequence defined recursively as follows: start with 0 and 1, and each subsequent term is the sum of the previous two. The first Fibonacci numbers are: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, …
- Source: [Wikipedia](https://en.wikipedia.org/wiki/Fibonacci_number)
{% endhint %}

## Start

Launch **Visual Studio**. Create a new project via **File > New > Project** or use the shortcut **Ctrl + Shift + N**. In the dialog choose: **Visual C# > Windows Universal > Blank App (Universal Windows)**. Name the project **Fibonacci 1.0**. From Solution Explorer open **MainPage.xaml** and **MainPage.xaml.cs**. If you don't see Solution Explorer, open it from **View > Solution Explorer** or use **Ctrl + W, S**.

## MainPage.xaml

The **MainPage.xaml** file contains the user interface markup written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
<!-- User Interface (UI): Fibonacci 1.0 -->
<StackPanel Background="Pink" Padding="50">
        
        <!-- Title -->
        <TextBlock Text="Fibonacci 1.0" FontSize="40" />

        <!-- Limit -->
        <TextBlock Text="Limit" Margin="0 10 0 10" FontSize="20" />
        <TextBox Name="boxLimit" FontSize="20" Text="1000" />
        <Button Content="Generate" Margin="0 10 0 10" Padding="20 10 20 10" FontSize="20"  Click="Button_Click" />
        
        <!-- Numbers -->
        <ListBox Name="boxNumbers"  Height="400" FontSize="20" />

</StackPanel>
```

Design view (XAML) in Visual Studio while developing the application:

![](/images/126_Fibonacci_1.0_UI.png)

_Fig. 1.26. UI design view_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the business logic written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): Fibonacci 1.0
public sealed partial class MainPage : Page
{
        // Collection
        private ObservableCollection<int> numbers = new ObservableCollection<int>();

        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
            boxNumbers.ItemsSource = numbers;
        }

        // Button Click Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            numbers.Add(1);
            numbers.Add(1);
            int limit = int.Parse(boxLimit.Text);
            int a = 1, b = 1, c = a + b;
            while (c < limit)
            {
                numbers.Add(c);
                a = b;
                b = c;
                c = a + b;
            }
        }
}
```

Business logic (C#) view in Visual Studio while developing the application:

![](/images/127_Fibonacci_1.0_BL.png)

_Fig. 1.27. Business logic view_

## Demo

Start the app via **Debug > Start Debugging** or press **F5**.

![](/images/128_Fibonacci_1.0_Run.png)

_Fig. 1.28. Universal app that generates numbers from the Fibonacci sequence._

