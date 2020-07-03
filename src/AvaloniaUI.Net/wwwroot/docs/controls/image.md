---
Title: Image
---
The `Image` control is a control for displaying raster images.

Binding on the `Image` control's `Source` property will not work unless you use a [binding converter](https://avaloniaui.net/docs/binding/converting-binding-values) that will convert a `string` into a `IBitmap`.

## Examples

### Swappable Image Button
An image button that changes images based on state is an example where binding to the `Image` control's `Source` property might seem necessary.

To have a button that swaps the image it's showing based on its state, you could either use a [binding converter](https://avaloniaui.net/docs/binding/converting-binding-values) that converts a `string` into a `IBitmap`, or you could use the declarative approaches below, which don't use binding.

The declarative approaches keep images in memory and won't have to load them in on-demand, which will net you greater performance than a binding approach. However, every image you use must be defined within the XAML.

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