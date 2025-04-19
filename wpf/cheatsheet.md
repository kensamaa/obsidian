
# WPF .NET Cheat Sheet

## Basic Concepts
- **WPF (Windows Presentation Foundation):** A UI framework for creating desktop client applications on Windows.
- **XAML (eXtensible Application Markup Language):** Declarative XML-based language for designing UI in WPF.
- **Data Binding:** Mechanism to bind UI elements to data sources.
- **MVVM (Model-View-ViewModel):** Design pattern for separating UI and business logic.

## Main Components
1. **Window**: Top-level container for a WPF application.
2. **Page**: Used for navigation within a window.
3. **UserControl**: Reusable component within Windows and Pages.
4. **Grid / StackPanel / DockPanel**: Layout containers for arranging child elements.

## XAML Basics
```xml
<Window x:Class="MyNamespace.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Grid>
        <!-- UI elements go here -->
    </Grid>
</Window>
````

### Common Controls



```xml
<Button Content="Click Me" Width="75" Height="23" Click="Button_Click"/>
<TextBox x:Name="myTextBox" Width="200"/>
<Label Content="Hello, World!"/>
<CheckBox Content="Check Me" IsChecked="False"/>
<ComboBox>
    <ComboBoxItem Content="Item 1"/>
    <ComboBoxItem Content="Item 2"/>
</ComboBox>
<ListBox>
    <ListBoxItem Content="Item A"/>
    <ListBoxItem Content="Item B"/>
</List>
```

### Layout Controls



```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>
    <TextBox Grid.Row="0" Text="Top"/>
    <TextBox Grid.Row="1" Text="Bottom"/>
</Grid>

<StackPanel>
    <Button Content="Button 1"/>
    <Button Content="Button 2"/>
</StackPanel>

<DockPanel>
    <Button Content="Top" DockPanel.Dock="Top"/>
    <Button Content="Bottom" DockPanel.Dock="Bottom"/>
    <Button Content="Left" DockPanel.Dock="Left"/>
    <Button Content="Right" DockPanel.Dock="Right"/>
    <Button Content="Fill"/>
</DockPanel>
```

## Events

### XAML Event Binding



```xml
<Button Content="Click Me" Click="Button_Click"/>
```

### Code-Behind Event Handler



```cs
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show("Button clicked!");
}
```

## Data Binding

### Simple Binding



```xml
<TextBox Text="{Binding MyProperty}"/>
```

### ViewModel Example



```cs
public class MyViewModel
{
    private string myProperty;
    public string MyProperty
    {
        get { return myProperty; }
        set { myProperty = value; }
    }
}
```

### Setting DataContext in Code-Behind



```cs
public MainWindow()
{
    InitializeComponent();
    DataContext = new MyViewModel();
}
```

## Styles and Resources



```xml
<Window.Resources>
    <Style TargetType="Button">
        <Setter Property="Background" Value="Blue"/>
        <Setter Property="Foreground" Value="White"/>
    </Style>
</Window.Resources>
```

## Commands

### XAML Command Binding



```xml
<Button Content="Save" Command="{Binding SaveCommand}"/>
```

### ViewModel Example



```cs
public ICommand SaveCommand { get; private set; }

public MyViewModel()
{
    SaveCommand = new RelayCommand(Save);
}

private void Save()
{
    // Implement save logic
}
```

### RelayCommand Implementation



```cs
public class RelayCommand : ICommand
{
    private readonly Action execute;
    private readonly Func<bool> canExecute;

    public RelayCommand(Action execute, Func<bool> canExecute = null)
    {
        this.execute = execute ?? throw new ArgumentNullException(nameof(execute));
        this.canExecute = canExecute;
    }

    public bool CanExecute(object parameter) => canExecute == null || canExecute();
    
    public void Execute(object parameter) => execute();
    
    public event EventHandler CanExecuteChanged
    {
        add => CommandManager.RequerySuggested += value;
        remove => CommandManager.RequerySuggested -= value;
    }
}
```

## Navigation

### Navigating to a Page



```cs
NavigationService.Navigate(new Uri("SecondPage.xaml", UriKind.Relative));
```



```text
---

You can  
```