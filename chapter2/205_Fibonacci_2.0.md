# Fibonacci 2.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a cross-platform mobile application to generate Fibonacci sequence numbers.

{% hint style='info' %}
#### Information
In mathematics, the Fibonacci numbers form a sequence defined recursively as follows: it starts with 0 and 1, and each subsequent term is the sum of the previous two. The first Fibonacci numbers are: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, …
- Source: [Wikipedia](https://en.wikipedia.org/wiki/Fibonacci_number)
{% endhint %}

## Start
1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Cross-Platform > Mobile App (Xamarin.Forms)**.
3. Name the project: **Fibonacci 2.0**.

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application

```xml
<!-- User Interface (UI): Fibonacci 2.0 -->
<StackLayout Padding="20">
        
    <!-- Title -->
    <Label Text="Fibonacci 2.0" FontSize="Large" />
        
    <!-- Limit -->
    <Label Text="Limit" />
    <Entry x:Name="boxLimit" Keyboard="Numeric" Text="1000" />
    <Button Text="Generate" Clicked="OnButtonClicked" />
        
    <!-- Numbers -->
    <ListView x:Name="boxNumbers" />
        
</StackLayout>
```

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the source code for the application's business logic and is written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): Fibonacci 2.0
public partial class MainPage : ContentPage
{
        // Constructor
        public MainPage()
        {
            InitializeComponent();
        }

        // Button Click Event Handler
        void OnButtonClicked(object sender, EventArgs args)
        {
            List<int> numbers = new List<int>();
            numbers.Add(1);
            numbers.Add(1);
            int limit = int.Parse(this.boxLimit.Text);
            int a = 1, b = 1, c = a + b;
            while (c < limit)
            {
                numbers.Add(c);
                a = b;
                b = c;
                c = a + b;
            }
            this.boxNumbers.ItemsSource = numbers;
        }
}
```

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/258_Fibonacci_2.0.png)

_Fig. 2.58 Testing the cross-platform mobile application for generating the Fibonacci sequence - Android Emulator 11 (API 30)_

