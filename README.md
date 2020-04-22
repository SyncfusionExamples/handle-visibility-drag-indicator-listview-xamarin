# How to show or hide drag indicator based on the DragStartMode in Xamarin.Forms ListView (SfListView)
You can handle the [DragIndicatorView](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.DragIndicatorView.html?) visibility based on [DragStartMode](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~DragStartMode.html?) by using the [converter](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/converters) in the Xamarin.Forms [SfListView](https://help.syncfusion.com/xamarin/listview/overview?).

You can also refer the following article.

https://www.syncfusion.com/kb/11425/how-to-show-or-hide-drag-indicator-based-on-the-dragstartmode-in-xamarin-forms-listview

**XAML**

Set the converter to the [IsVisible](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.DragIndicatorView~IsVisible.html?) property of **DragIndicatorView**.
``` xml
<syncfusion:SfListView x:Name="listView" Grid.Row="1" ItemSize="60" BackgroundColor="#FFE8E8EC" GroupHeaderSize="50" ItemsSource="{Binding ToDoList}" DragStartMode="OnHold" SelectionMode="None">
    <syncfusion:SfListView.ItemTemplate>
        <DataTemplate>
            <Frame HasShadow="True" BackgroundColor="White" Padding="0">
                <Frame.InputTransparent>
                    <OnPlatform x:TypeArguments="x:Boolean" Android="True" WinPhone="False" iOS="False"/>
                </Frame.InputTransparent>
                <Grid>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition Width="*" />
                        <ColumnDefinition Width="60" />
                    </Grid.ColumnDefinitions>
                    <Label x:Name="textLabel" Text="{Binding Name}" FontSize="15" TextColor="#333333" VerticalOptions="Center" HorizontalOptions="Start" Margin="5,0,0,0" />
                    <syncfusion:DragIndicatorView Grid.Column="1" ListView="{x:Reference listView}" HorizontalOptions="Center" VerticalOptions="Center" IsVisible="{Binding DragStartMode, Source={x:Reference listView},Converter={StaticResource dragValueConverter}}">
                        <Grid Padding="10, 20, 20, 20">
                            <Image Source="DragIndicator.png" VerticalOptions="Center" HorizontalOptions="Center" />
                        </Grid>
                    </syncfusion:DragIndicatorView>
                </Grid>
            </Frame>
        </DataTemplate>
    </syncfusion:SfListView.ItemTemplate>
</syncfusion:SfListView>
```
**C#**

Converter to return true or false based on the **DragStartMode**.
``` c#
namespace ListViewXamarin
{
    public class DragValueConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            var dragMode = (DragStartMode)value;
            if (dragMode == DragStartMode.OnHold || dragMode == DragStartMode.OnDragIndicator)
                return true;
            else
                return false;
        }
 
        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            throw new NotImplementedException();
        }
    }
}
```
