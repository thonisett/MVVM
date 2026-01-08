## This section shows how the view model and UI layers update each other.

This scenario shows how text entered into an Entry element can be added to a CollectionView after click on the add button

![Alt text](/Assets/Add_new_item.png "Adding item to Entry")
*Adding item to Entry*


![Alt text](/Assets/New_item_added.png "Items added to CollectionView")
*Items added to CollectionView*

# Steps how this works

1.  Add Entry element to the view.  This is where the user adds a item to the shopping list
```
<Entry
    Grid.Row="2"
    Grid.Column="0"
    Placeholder="Enter Item"
    Text="{Binding ShoppingItem}" />
```


2.  Add a CollectionView to the View.  This shows all the items added to the Entry element

'''
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

'''
