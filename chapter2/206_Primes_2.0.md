# Primes 2.0

Using the Visual Studio integrated development environment and the C# programming language, we will develop a cross-platform mobile application to generate a sequence of prime numbers.

{% hint style='info' %}
#### Information
A prime number is a natural number greater than 1 that is not a product of two smaller natural numbers.
- Source: [Wikipedia](https://en.wikipedia.org/wiki/Prime_number)
{% endhint %}

## Start

1. Launch the Visual Studio integrated development environment.
2. Create a new project: **Visual C# > Cross-Platform > Mobile App (Xamarin.Forms)**.
3. Name the project: **Primes 2.0**.

## MainPage.xaml

The **MainPage.xaml** file contains the source code for the application's user interface design and is written in XAML. Copy (Ctrl+C) and paste (Ctrl+V) the fragment below into your application

```xml
<!-- User Interface (UI): Primes 2.0 -->
<StackLayout Padding="20" BackgroundColor="Yellow">
        
    <!-- Title -->
    <Label Text="Primes 2.0" FontSize="Large" />

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
// Business Logic (BL): Primes 2.0
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
            List<int> primes = new List<int>();
            int limit = int.Parse(this.boxLimit.Text);
            for (int k = 2; k < limit; k++)
            {
                bool prime = true;
                for (int j = 2; j < k; j++) if (k % j == 0) prime = false;
                if (prime) primes.Add(k);
            }
            this.boxNumbers.ItemsSource = primes;
        }
}
```

## Demo

Run the application from the menu: **Debug > Start Debugging** or by pressing the **F5** key.

![](/images/259_Primes_2.0.png)

_Fig. 2.59 Testing the cross-platform mobile application for generating a sequence of prime numbers - Android Emulator 11 (API 30)_

