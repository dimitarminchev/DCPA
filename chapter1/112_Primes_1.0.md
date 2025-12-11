# Primes 1.0

Using Visual Studio and C# we will build a Universal Windows Platform application that generates a sequence of prime numbers.

{% hint style='info' %}
#### Info
A prime number is a natural number greater than 1 that has no positive divisors other than 1 and itself.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/Prime_number)
{% endhint %}


## Start

1. Launch **Visual Studio**.
2. Create a new project: **Visual C# > Windows Universal > Blank App (Universal Windows)**.
3. Name the project **Primes 1.0**.

## MainPage.xaml

The **MainPage.xaml** file contains the user interface markup written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```xml
<!-- User Interface (UI): Primes 1.0 -->
<StackPanel Background="Yellow" Padding="50">

        <!-- Title -->
        <TextBlock Text="Primes 1.0" FontSize="40" />
        
        <!-- Limit -->
        <TextBlock Text="Limit" FontSize="20" />
        <TextBox Name="boxLimit" Text="1000" FontSize="20" />
        <Button Content="Generate" Margin="0 10 0 10" Padding="20 10 20 10" FontSize="20"  Click="Button_Click" />
        
        <!-- Numbers -->
        <ListBox Name="boxNumbers" Height="400" FontSize="20" />
        
</StackPanel>
```

Design view (XAML) in Visual Studio while developing the application:

![](/images/129_Primes_1.0_UI.png)

_Fig. 1.29. UI design view_

## MainPage.xaml.cs

The **MainPage.xaml.cs** file contains the business logic written in C#. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application.

```csharp
// Business Logic (BL): Primes 1.0
public sealed partial class MainPage : Page
{
        // Constructor
        public MainPage()
        {
            this.InitializeComponent();
        }

        // Button Event Handler
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            int limit = int.Parse(boxLimit.Text);
            for (int k = 2; k < limit; k++)
            {
                bool prime = true;
                for (int j = 2; j < k; j++) if (k % j == 0) prime = false;
                if (prime) boxNumbers.Items.Add(k);
            }
        }
}
```

Business logic (C#) view in Visual Studio while developing the application:

![](/images/130_Primes_1.0_BL.png)

_Fig. 1.30. Business logic view_

## Demo

Start the app via **Debug > Start Debugging** or press **F5**.

![](/images/131_Primes_1.0_Run.png)

_Fig. 1.31. Universal app that generates a sequence of prime numbers._

