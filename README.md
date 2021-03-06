# DefOS
Extra native OS functions for games written using the Defold game engine

Currently uses Native Extension for macOS, Windows and HTML5. Contribute!

## Installation
You can use DefOS in your own project by adding this project as a [Defold library dependency](http://www.defold.com/manuals/libraries/). Open your game.project file and in the dependencies field under project add:

https://github.com/subsoap/defos/archive/master.zip

## Methods

Customize title bar accessories and title.

```lua
defos.disable_maximize_button()
defos.disable_minimize_button()
defos.disable_window_resize()
defos.set_window_title("I set this title using Defos")
```

---

Toggle window maximize status.

```lua
defos.set_maximized(bool_value)
defos.toggle_maximized()
bool_value = defos.is_maximized()
```

---

Toggle full screen. On HTML5, this only works from `defos.on_click()`.

```lua
defos.set_fullscreen(bool_value)
defos.toggle_fullscreen()
bool_value = defos.is_fullscreen()
```

---

Get/set the window's size and position in screen coordinates. The window area
includes the title bar, so the actual contained game view area might be smaller
than the given metrics.

Passing `nil` for `x` and `y` will center the window in the middle of the display.

Screen coordinates start at (0, 0) in the top-left corner of the main display.
X axis goes right. Y axis goes down.

```lua
x, y, w, h = defos.get_window_size()
defos.set_window_size(x, y, w, h)
```

---

Get/set the game view size and position in screen coordinates. This adjusts
the window so that its containing game view is at the desired size and position.
The window will be larger than the given metrics because it includes the title
bar.

Passing `nil` for `x` and `y` will center the window in the middle of the display.

```lua
x, y, w, h = defos.get_view_size()
defos.set_view_size(x, y, w, h)
```

---

Show/hide the mouse cursor.

```lua
defos.set_cursor_visible(bool_value)
bool_value = defos.is_cursor_visible()
```

---

Respond to the mouse entering and leaving the game view area.

```lua
bool_value = defos.is_mouse_in_view()
defos.on_mouse_enter(function ()
  print("Mouse entered view")
end)
defos.on_mouse_leave(function ()
  print("Mouse left view")
end)
```

---

Move the cursor programatically.

```lua
defos.set_cursor_pos(x, y) -- In screen coordinates
defos.move_cursor_to(x, y) -- In game view coordinates
```

---

Clip cursor to current game view area. Windows only.

```lua
defos.set_cursor_clipped(bool_value)
bool_value = defos.is_cursor_clipped()
```

---

Lock cursor movement. On HTML5 this only works from `defos.on_click()`.

```lua
defos.set_cursor_locked(bool_value)
bool_value = defos.is_cursor_locked()
defos.on_cursor_lock_disabled(function ()
  print("Called on HTML5 when the user presses ESC and the browser disables locking");
end)
```

---

Set custom hardware cursors. `cursor` can be one of the following:
  * `nil`: Resets the cursor to default. Equivalent to `defos.reset_cursor()`.
  * `defos.CURSOR_ARROW`
  * `defos.CURSOR_HAND`
  * `defos.CURSOR_CROSSHAIR`
  * `defos.CURSOR_IBEAM`
  * On HTML5, an URL to an image (data URLs work as well)
  * On Windows, a path to an `.ani` or `.cur` file on the file system.
  * On macOS, a table of the form:  
  ```lua
  {
    image = resource.load("cursor.tiff"),
    hot_spot_x = 18,
    hot_spot_y = 2,
  }
  ```

On macOS, custom cursors can be any image file supported by `NSImage`, but it's highly recommended to
[create a TIFF](https://developer.apple.com/library/content/documentation/GraphicsAnimation/Conceptual/HighResolutionOSX/Optimizing/Optimizing.html#//apple_ref/doc/uid/TP40012302-CH7-SW27)
with two images, one at 72DPI (for low density displays) and another at 144DPI (for Retina displays).

The hotspot is an anchor point within the image that will overlap with the functional position of the mouse pointer (eg. the tip of the arrow).

```lua
defos.set_cursor(cursor)
defos.reset_cursor()
```

---

On Windows only, show/hide the console window. Only works when not running
from the Editor.

```lua
defos.set_console_visible(bool_value)
bool_value = defos.is_console_visible()
```

---

On HTML5 only, get a synchronous event when the user clicks in the canvas.
This is necessary because some HTML5 functions only work when called
synchronously from an event handler.

This is currently needed for:
* `defos.toggle_fullscreen()`
* `defos.set_cursor_locked(true)`

```lua
defos.on_click(function ()
  print("The user has clicked. I have the chance to respond synchronously")
end)
```

---

If you'd like to see any other feature, open an issue.

## Example
An example is made using [DirtyLarry](https://github.com/andsve/dirtylarry)
![Defos example screenshot](https://github.com/subsoap/defos/raw/master/docs/example_screenshot.jpg)
