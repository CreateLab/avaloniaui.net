---
Title: Image
---
The `Image` control is a control for displaying raster images.

Binding on the `Image` control's `Source` property will not work unless you use a [binding converter](https://avaloniaui.net/docs/binding/converting-binding-values) that will convert a `string` into a `IBitmap`.

## Examples
### Swappable Image Button
To have a button that swaps the image it's showing based on its state, you could either use a [binding converter](https://avaloniaui.net/docs/binding/converting-binding-values) that converts a `string` into a `IBitmap`, or you can use the declarative approach, as shown below.

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

## Source code
[Image.cs](https://github.com/AvaloniaUI/Avalonia/blob/master/src/Avalonia.Controls/Image.cs)
