This section shows how the view and viewmodel works to display shopping items that have been entered into the CreateListView

Views are the UI's that are written in XAML. Unlike prevous .NET UIs, such as WinForms and WPFs, MAUI strongly discourages any code logic to sit in the .xaml.cs files. Instead, it is
the role of the ViewModel to manage how data is provided to the View.  Keeping logic code from the View maintains the principles of separation of concerns.

Each view has its own ViewModel file.

The invidual UI elements, such as Entry and CollectionView, communicates to the CreateViewModel with the use of bindings.

![Alt text](/Assets/FileStructure.png "a title")

Layout of Shopping List Project 

It is vial that the top of the View file contains information that allows it to link with the View Model

```
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:vm="clr-namespace:Shopping_List.ViewModel"
             x:Class="Shopping_List.Views.CreateListView"
             x:DataType="vm:CreateListViewModel"
             Title="Create and View Shopping list">

```
 The following lines are broken down for more information

The information on the schemas is boiler plate code that does not change
```
xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
```

This provides the namespace to the folder in which all the ViewModels are kept
```
xmlns:vm="clr-namespace:Shopping_List.ViewModel"

```
The x:Class direcive configures XAML markup compilation to join partial classes between the markup and code behind
```
x:Class="Shopping_List.Views.CreateListView"
```
The x:DataType allows the visual mapping of the data bindings between the View and ViewModel 
```
x:DataType="vm:CreateListViewModel"
```

This sets the title for the view page
```
Title="Create and View Shopping list
```

Layout of the CreateListViewModel

```
using CommunityToolkit.Mvvm.ComponentModel;
using CommunityToolkit.Mvvm.Input;
using System.Collections.ObjectModel;

namespace Shopping_List.ViewModel
{
    public partial class CreateListViewModel : ObservableObject
    {


        [ObservableProperty]
        private ObservableCollection<string> items = new();

        [ObservableProperty]
        string? shoppingItem;

        [RelayCommand]
        public void AddToList()
        {
            Items.Add(ShoppingItem);
            ShoppingItem = string.Empty;
        }
    }
}
```
Layout of View

```
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:vm="clr-namespace:Shopping_List.ViewModel"
             x:Class="Shopping_List.Views.CreateListView"
             x:DataType="vm:CreateListViewModel"
             Title="Create and View Shopping list">


    <Grid ColumnSpacing="12"
          RowSpacing="16"
          Padding="20">

        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>

        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Star"/>
            <ColumnDefinition Width="Star"/>
            <ColumnDefinition Width="Star"/>

        </Grid.ColumnDefinitions>


        <Label Grid.Row="0"
               Grid.Column="0"
               Text="Select Date"
               VerticalOptions="Center"/>

        <DatePicker Grid.Row="0"
                    Grid.Column="1"
                    VerticalOptions="Center"/>

    
        <Label Grid.Row="1"
               Grid.Column="0"
               Text="Shop"
               VerticalOptions="Center"/>

        <Entry Grid.Row="1"
               Grid.Column="1"
               Placeholder="Enter shop"
               VerticalOptions="Center"/>

        <Entry
            Grid.Row="2"
            Grid.Column="0"
            Placeholder="Enter Item"
            Text="{Binding ShoppingItem}" />

        <Button Grid.Row="2"
                Grid.Column="1"
                Text="Add Item"
                VerticalOptions="Center"
                Command="{Binding AddToListCommand}"/>


        <CollectionView
            Grid.Row="3"
            Grid.ColumnSpan="3"
            ItemsSource="{Binding Items}">

            <CollectionView.ItemTemplate>
                <DataTemplate x:DataType="{x:Type x:String}">
                    <Grid Padding="0,5">
                        <Border>
                            <Label Text="{Binding .}"
                               FontSize="18"
                               Padding="8"/>
                            
                        </Border>
                    </Grid>
                    
                </DataTemplate>
            </CollectionView.ItemTemplate>

        </CollectionView>

    </Grid>

</ContentPage>
```
