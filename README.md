# DefOS
Extra native OS functions for games written using the Defold game engine

Currently uses FFI for Windows and Native Extension for macos, but when Native Extensions are released for all platforms will likely switch to that. Contribute!

## Installation
You can use DefOS in your own project by adding this project as a [Defold library dependency](http://www.defold.com/manuals/libraries/). Open your game.project file and in the dependencies field under project add:

	https://github.com/subsoap/defos/archive/master.zip
### Windows
Once added, you must require the main Lua module via
```
local defos = require("defos.defos") --windows only!!!
```
"require" - used only on Windows.

By using the dependency version, you can more easily update the module, but you may wish to keep it static. You can also download the defos.lua module file and add it to a utils folder. Then you would require via

```
local defos = require("utils.defos") --windows only!!!
```
### macos
Just make Installation. Than you can use "defos" global module.

## Methods

Then you can use the module in the script including the module via

```
function init(self)
	defos.disable_maximize_button()
	defos.disable_minimize_button()
	defos.disable_window_resize()
	defos.disable_mouse_cursor()
	defos.enable_mouse_cursor()
	defos.set_window_size(-1,-1,800,600)
end
```
Use issues for feature requests.