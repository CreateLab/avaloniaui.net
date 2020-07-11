---
Title: ToggleButton
---
The `ToggleButton` control is a subclass of the `Button` control that has a built-in `checked` state. This means the button can be checked or unchecked on click by a user. You may change the styling of controls based on whether `ToggleButton` is checked or not by using the `:checked` [pseudoclass.](https://avaloniaui.net/docs/styles/styles#pseudoclasses)

## Source code
[ToggleButton.cs](https://github.com/AvaloniaUI/Avalonia/blob/master/src/Avalonia.Controls/ToggleButton.cs)

## Examples

### Speaker Mute Button
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
