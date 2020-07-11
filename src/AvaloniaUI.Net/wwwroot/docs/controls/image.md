---
Title: Image
---
The `Image` control is a control for displaying raster images.

## Binding
Binding onto an `Image` control's `Source` property with a string must be done using a [binding converter](https://avaloniaui.net/docs/binding/converting-binding-values) that will convert the `string` to an `IBitmap`.

## Subclasses
1. [DrawingPresenter](https://avaloniaui.net/docs/controls/drawingpresenter) - Used to display svgs.

## Examples

### Swappable Image Button
An image button that changes images based on state is an example where binding to the `Image` control's `Source` property might seem necessary.

To have a button that swaps the image it's showing based on its state, you could either use a [binding converter](https://avaloniaui.net/docs/binding/converting-binding-values) that converts a `string` into a `IBitmap`, or you could use the declarative approaches below, which don't use binding.

The declarative approaches keep images in memory and won't have to load them in on-demand, which will net you greater performance than a binding approach. However, every image you use must be defined within the XAML.

#### Binding Converter Approach
```xml
<UserControl.Resources>
    <ext:BitmapAssetValueConverter x:Key="variableImage"/>
</UserControl.Resources>
```

```xml
<Image Width="75"
       Height="73"
       Source="{Binding PlaySource, Converter={StaticResource variableImage}}">
```

```csharp
/// <summary>
/// <para>
/// Converts a string path to a bitmap asset.
/// </para>
/// <para>
/// The asset must be in the same assembly as the program. If it isn't,
/// specify "avares://<assemblynamehere>/" in front of the path to the asset.
/// </para>
/// </summary>
public class BitmapAssetValueConverter : IValueConverter
{
    public static BitmapAssetValueConverter Instance = new BitmapAssetValueConverter();

    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        if (value == null)
            return null;

        if (value is string rawUri && targetType == typeof(IBitmap))
        {
            Uri uri;

            // Allow for assembly overrides
            if (rawUri.StartsWith("avares://"))
            {
                uri = new Uri(rawUri);
            }
            else
            {
                string assemblyName = Assembly.GetEntryAssembly().GetName().Name;
                uri = new Uri($"avares://{assemblyName}{rawUri}");
            }

            var assets = AvaloniaLocator.Current.GetService<IAssetLoader>();
            var asset = assets.Open(uri);

            return new Bitmap(asset);
        }

        throw new NotSupportedException();
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotSupportedException();
    }
}
```

#### Declarative Approaches

##### Using a Button
```
<Button Name="PlayButton" HorizontalAlignment="Center" Width="36" Command="{Binding PlayCommand}">
    <Panel>
        <Image Source="{DynamicResource Play}" IsVisible="{Binding !IsPlaying}" Width="20"
                          Height="20" VerticalAlignment="Center" HorizontalAlignment="Center" />
        <Image Source="{DynamicResource Pause}" IsVisible="{Binding IsPlaying}" Width="20"
                          Height="20" VerticalAlignment="Center" HorizontalAlignment="Center" />
    </Panel>
</Button>
```

##### Using a ToggleButton
```
<Style Selector="ToggleButton DrawingPresenter.tbchecked">
    <Setter Property="IsVisible" Value="false"/>
</Style>
<Style Selector="ToggleButton:checked DrawingPresenter.tbchecked">
    <Setter Property="IsVisible" Value="true"/>
</Style>
<Style Selector="ToggleButton DrawingPresenter.tbunchecked">
    <Setter Property="IsVisible" Value="true"/>
</Style>
<Style Selector="ToggleButton:checked DrawingPresenter.tbunchecked">
    <Setter Property="IsVisible" Value="false"/>
</Style>
```

```
<ToggleButton Classes="vtrx"  IsChecked="{Binding Path=vtrx.muted}" ToolTip.Tip="stop audio" >
    <Panel>
        <DrawingPresenter Drawing="{DynamicResource Icon.Speaker}" />
        <DrawingPresenter Width="14" Height="14" Margin="14,14,0,0" Drawing="{DynamicResource Icon.SpeakerMute}" Classes="tbchecked"/>
    </Panel>
</ToggleButton>
```

## Source code
[Image.cs](https://github.com/AvaloniaUI/Avalonia/blob/master/src/Avalonia.Controls/Image.cs)