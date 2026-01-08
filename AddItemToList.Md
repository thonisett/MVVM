This section shows how the view and viewmodel works to display shopping items that have been entered into the CreateListView

Views are the UI's that are written in XAML. Unlike prevous .NET UIs, such as WinForms and WPFs, MAUI strongly discourages any code logic to sit in the .xaml.cs files. Instead, it is
the role of the ViewModel to manage how data is provided to the View.  Keeping logic code from the View maintains the principles of separation of concerns.

Each view has its own ViewModel file.

The invidual UI elements, such as Entry and CollectionView, communicates to the CreateViewModel with the use of bindings.

![Alt text](/Assets/FileStructure.png "a title")
** Layout of Shopping List Project **

It is vial that the top of the View file contains information that allows it to link with the View Model

```
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:vm="clr-namespace:Shopping_List.ViewModel"
             x:Class="Shopping_List.Views.CreateListView"
             x:DataType="vm:CreateListViewModel"
             Title="Create and View Shopping list">

```

