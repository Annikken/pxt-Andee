# Andee

This PXT package is to enable the use of the Annikken Andee app on the BBC micro:bit. Users can create UI widgets like sliders, buttons and more to control the micro:bit using their BLE enabled smartphone/tablets.
This package has been updated to support the increased storage of the microbit V2. 

## Getting Started with Andee on micro:bit

No extra hardware is required to use Andee on the micro:bit. Andee uses the BLE that is already present on the micro:bit. Andee might not be compatible with other packages running BLE

Andee can be used either with the paired connection or the unpaired one. We recommend using the paired connection especially when there are multiple micro:bits running Andee in close proximity to each other.

[For more information about how Bluetooth pairing on the micro:bit works and how to pair,click here](https://makecode.microbit.org/reference/bluetooth/bluetooth-pairing)

If you are unable to pair your micro:bit to your mobile device or would prefer not to pair the micro:bit to your device, you can follow the steps below:
1. In the Makecode editor, click on the gear icon on the right hand corner of the window
2. Click on `Project Settings` 
3. Click the switch that says `No Pairing Required: Anyone can connect via Bluetooth.`
4. Then click `Save`

The Andee app will now be able to scan and detect your micro:bit 

**For video examples on how to get started with Andee and create the widgets, [click here](https://www.annikken.com/micro-bit/get-started)**

---
## Basic Usage

### Begin

The ``||Andee.begin()||`` block is required to start using Andee widgets

```blocks
Andee.begin();
```
---
### Creating Widgets
	
These are examples on how to create each type of widget that Andee supports.
For explanation on all the properties of the widget [look here.](#parameter)

#### Data Widget
```blocks
let widget = Andee.createWidget(
WidgetId.Widget_1,
WidgetType.Databox,
WidgetPosition.Row0_Column0,
WidgetLength.Half,
WidgetColour.Red,
"Title",
"Data",
"Units"
);
```
[How the widget looks](https://annikken.gitbooks.io/annikken-andee/content/About/uiType.html#databox)

#### Circular Data Widget
```blocks
let widget = Andee.createWidget(
WidgetId.Widget_1,
WidgetType.Databox_Circle,
WidgetPosition.Row0_Column0,
WidgetLength.Half,
WidgetColour.Red,
"Title",
"Data",
"Units"
);
```
[How the widget looks]()


#### Header Widget
```blocks
let widget = Andee.createWidget(
WidgetId.Widget_1,
WidgetType.Databox_Header,
WidgetPosition.Row0_Column0,
WidgetLength.Half,
WidgetColour.Red,
"Title",
"Not Used",
"Not Used"
);
```
[How the widget looks]()

#### Button Widget
```blocks
let widget = Andee.createWidget(
WidgetId.Widget_1,
WidgetType.Databox,
WidgetPosition.Row0_Column0,
WidgetLength.Half,
WidgetColour.Red,
"Title",
"Data",
"Units"
);
```
[How the widget looks](https://annikken.gitbooks.io/annikken-andee/content/About/uiType.html#button)

#### Circle Button Widget
```blocks
let widget = Andee.createWidget(
WidgetId.Widget_1,
WidgetType.Button_Circle,
WidgetPosition.Row0_Column0,
WidgetLength.Half,
WidgetColour.Red,
"Title",
"Data",
"Units"
);
```
[How the widget looks]()

#### Keyboard Input Widget
```blocks
let widget = Andee.createWidget(
WidgetId.Widget_1,
WidgetType.Keyboard_In,
WidgetPosition.Row0_Column0,
WidgetLength.Half,
WidgetColour.Red,
"Title",
"Data",
"Units"
);
```
[How the widget looks](https://annikken.gitbooks.io/annikken-andee/content/About/uiType.html#keyboard)

#### Slider Widget
```blocks
let widget = Andee.createSliderWidget(
WidgetId.Widget_1,
WidgetTypeInput.Slider,
WidgetPosition.Row0_Column0,
WidgetLength.Full,
WidgetColour.Red,
"Title",
"Units",
"0",
"100",
"0",
100
);
```
[How the widget looks](https://annikken.gitbooks.io/annikken-andee/content/About/uiType.html#slider)

#### Analog Circle Widget
```blocks
let widget = Andee.createSliderWidget(
WidgetId.Widget_1,
WidgetTypeInput.Analog_Dial,
WidgetPosition.Row0_Column0,
WidgetLength.Full,
WidgetColour.Red,
"Title",
"Units",
"0",
"100",
"0",
100
);
```
[How the widget looks](https://annikken.gitbooks.io/annikken-andee/content/About/uiType.html#analog)

---
### Displaying the widgets

Once the widget parameters have been set, the block ``||widget.update()||`` has to be used for each widget created.This block will tell the app to draw out the widget or update it. 
```blocks
basic.forever(() => {
    widget.update()
})
```
---
### Andee Events

This block is used to create triggers for widgets like buttons, sliders and keyboard. Users can specify the actions to be done when the events are triggered. Each event will be shown below. 

#### Button Events

Button events work for both normal and circle buttons. For example, if a button widget with id 2 has been created, the event block needed is
```blocks
Andee.WidgetEvent(WidgetId.Widget_2, () => {
});
```

#### Slider Events
```blocks
Andee.WidgetEvent(WidgetId.Widget_3, () => {
	let reply = Andee.getSlider();
});
```
*Note: For sliders, a variable has to be created to store the value from the slider widget. ``||Andee.getSlider()||`` returns a `number`*

#### Keyboard Input Events
```blocks
Andee.WidgetEvent(WidgetId.Widget_1, () => {
	let reply = Andee.getKeyboard();
	widget.ack();
});
```
*Note: For keyboard input, a variable has to be created to store the string from the Keyboard widget. ``||Andee.getKeyboard()||`` returns a `string`*

---
Each widget has a few properties that can be customised. {parameter}
The properties are
1. **ID** Each widget requires a unique number ID   
  2. **Type** This specifies whether a widget is a button, slider etc
  3. **Length** This enables the user to use shorter widths and fit more widgets in a row
  4. **Colour** This variable changes the color of the widget
  5. **Title** Text located in the widget
  6. **Data** Text located in the widget
  7. **Units** Text located in the widget
  8. **Position** This variable controls the position of the widget in the app. In Makecode, when the position dropdown is clicked, there will be a table with 4 rows and columns. The widget will appear in the location the user specify.
---
## Advanced Usage

### Changing Widget Properties 

The blocks below are used to change the properties of a widget while the sketch is running. This enables the user to create e a more interactive UI.

Every time a widget property is changed, ``||widget.update()||`` has to be called for the changes to take place in the app. The widget property can be changed in an event or in the ``Forever`` loop.

#### Set Widget Title
This block changes the title of the widget and only accepts a `string`
```blocks
basic.forever(() => {
    widget.setTitle("Title");
    widget.update();
})
```

#### Set Widget Data
This block changes the data section of the widget and only accepts a `string`
```blocks
basic.forever(() => {
    widget.setData("Data");
    widget.update();
})
```

#### Set Widget Units
This block changes the units section of the widget and only accepts a `string`
```blocks
basic.forever(() => {
    widget.setUnit("Units");
    widget.update();
})
```

#### Set Widget Colour
This block changes the colour of the widget
```blocks
basic.forever(() => {
	widget.setColour(WidgetColour.Red)
	widget.update();
})
```

#### Set Widget Width
This block changes the width of the widget with a `number` of range 0 to 100
```blocks
basic.forever(() => {
	widget.setWidth(50)
	widget.update();
})
```

#### Set Widget Height
This block changes the height of the widget with a `number` of range 0 to 100
```blocks
basic.forever(() => {
	widget.setHeight(25)
	widget.update();
})
```

#### Set Coordinate X of Widget
This block changes the X coordinate of the top-left hand corner of the widget with a `number` of range 0 to 100. 
```blocks
basic.forever(() => {
	widget.setCoordX(50)
	widget.update();
})
```

#### Set Coordinate Y of Widget
This block changes the Y coordinate of the top-left hand corner of the widget with a `number` of range 0 to 100. 
```blocks
basic.forever(() => {
	widget.setCoordY(50)
	widget.update();
})
```

#### Set Keyboard Mode
This block changes the keyboard layout to either AlphaNumeric or Numeric keyboard. Default mode is the AlphaNumeric keyboard
```blocks
basic.forever(() => {
	widget.setKeyboardInputMode(KeyboardMode.AlphaNumeric)
	widget.update();
})
```

#### Set Slider Mode
This block changes the input mode of the slider to either "register value on finger release" or "register value on change". Default mode is "register value on finger release"
```blocks
basic.forever(() => {
	widget.setSliderInputMode(SliderMode.On_Finger_Release)
	widget.update();
})
```

#### Set Button Mode
This block changes the button to either unpress immediately or wait for an acknowledgment before unpressing itself. Default mode is to unpress immediately
```blocks
basic.forever(() => {
	widget.setButtonInputMode(ButtonMode.Acknowledge)
	widget.update();
})
```

---
### Button is pressed more than once
This block will return `true` if the button widget has been pressed more than once and will return `false` when not. 

In this example, the happy face icon will show on the LED array on the microbit when the button is pressed twice, while pressing the button once will show a sad face icon
```blocks
Andee.WidgetEvent(WidgetId.Widget_2, () => {
    if (Andee.getButtonPress()) {
        basic.showIcon(IconNames.Happy)
    } else {
        basic.showIcon(IconNames.Sad)
    }
})
```
---
### Update Widget every ___ loops
This block will cause the widget to send an update after a specified number of loops have passed. All widgets will update after 100 loops as a default. If a more frequent update is required for faster response, this block should be used
```blocks
basic.forever(() => {
	widget.updateLoop(50)
})
```
---
### Force Widget update
This block forces the widget to update immediately
```blocks
basic.forever(() => {
	widget.forceUpdate()
})
```
---
### Convert to String
This block converts numbers to `string`. Usually used when a number is needed to be displayed on ``||widget.setData()||`` , ``||widget.setTitle()||`` or ``||widget.setUnit()||``
```blocks
basic.forever(() => {
	let value = 50;
	widget.setData(Andee.convertNumberToString(value));
})
```
---
### Clear All widgets
This block will clear all widgets in the app. Use ``||widget.update()||`` block to display the widgets again
```blocks
basic.forever(() => {
	Andee.clear()
})
```
---
### Remove Widget
This block will clear a widget one at a time
```blocks
basic.forever(() => {
	widget.remove()
})
```
  
---
## Supported targets

* for PXT/microbit

## License

MIT

