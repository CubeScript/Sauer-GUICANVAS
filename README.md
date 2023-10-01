## Cube 2 Sauerbraten Canvas Interface
GUICANVAS is a set of commands for [Sauerbraten](http://sauerbraten.org/) that allows you to draw pixels in GUI menus using CubeScript.

![](https://github.com/SalatielSauer/misc/blob/master/guicanvas_notepad_1.gif)

### Installation
1. Download [guicanvas.zip](https://github.com/CubeScript/Sauer-GUICANVAS/releases/latest) (without extracting it).
2. Move the zip to the Sauerbraten home folder (or the main installation folder).
3. Find your autoexec.cfg file or create a new one (also in one of the root folders), open it in a text editor and add the following commands:
`addzip guicanvas.zip; exec guicanvas.cfg`<br>
The zip will be extracted internally and the configuration file (guicanvas.cfg) will be applied whenever you start the game.

Alternatively to step 3 you can type the command `/notepad autoexec.cfg` during the game to open the built-in text editor.

<hr>

### Playable Demos
![](https://github.com/SalatielSauer/misc/blob/master/guicanvas_snake_1.gif)

Currently the installation zip comes with the demos below that you can run and test:
- [guicanvas_snake.cfg](https://github.com/CubeScript/Sauer-GUICANVAS/blob/main/guicanvas/guicanvas_snake.cfg) by [@SalatielSauer](https://github.com/SalatielSauer)
- [guicanvas_raycast.cfg](https://github.com/CubeScript/Sauer-GUICANVAS/blob/main/guicanvas/guicanvas_raycast.cfg) by [@SalatielSauer](https://github.com/SalatielSauer)

feel free to contribute more :)

Note: Some GUICANVAS demos are expected to replace key binds such as directional arrows.

<hr>

### How it works
Behind the scenes GUICANVAS uses .obj mapmodels as *screens*, each pixel is a mesh whose name corresponds to its position (index) in the 2D plane. The model command to define skins by meshes (in this case `objskin`) is extremely fast, allowing us to easily update their colors or textures.

For the front end, GUICANVAS uses the `guimodelpreview` command, which allows us to register and display any mapmodel with a given size and even an animation state.

Another important command is `guistrut`, with it we can overlay GUI elements and make the magic work.

If you are not into menus or want to create your own physical arcade, you can spawn the screen using the `/newent mapmodel $nummapmodels; mmodel guicanvas` command in edit mode.

<hr>

### GUICANVAS Custom Commands
`guicanvas.cfg` has some commands and variables that you can use.

### `guicanvas.setPixel x y r g b`
This is the main command to add a pixel before drawing it, `x` refers to the horizontal line and `y` to the vertical, `r` `g` `b` are the colors ranging between 0-1.

If `r` is set to -1 the pixel will be displayed with complete opacity;

If `r` is a string it will be treated as a texture path.

### `guicanvas.fillRect x y width height r g b`
This is a helper function that uses `guicanvas.setPixels` to fill a square with a given size `width` `height` at a given `x` `y` position.

### `guicanvas.refresh`
This is the command to actually draw the screen from the list of added pixels (`$guicanvas.pixels`), it will also clear the list unless `guicanvas.keepPixels` is set to 1.

### `guicanvas.onupdate = [action]`
Works as an event hook, the contents of `$guicanvas.onupdate` are executed every millisecond set by `$guicanvas.refreshRate`.

### `guicanvas.play [action] [interface] x y`
This is the main command for creating and displaying the GUI menu, with extra functions to facilitate the positioning of other GUI elements.

`action` has the same effect as `$guicanvas.onupdate`, its content is executed every millisecond defined by `$guicanvas.refreshRate`;

`interface` is where you can include other GUI elements that you want to see on the screen (guitext, guititle, guibutton...), they are positioned by default at 0 0 unless determined by `x` and `y`.

Careful and extensive use of `guistrut` may be necessary if you wish to hide the original background (the guiskin), which may appear depending on the lenght of your text elements, take a look at the demo files to get an idea of ​​how to correct these.

Alternatively you can always create your own menu using the guimodelpreview command to display the screen.

### `guicanvas.perspective pitch fov`
This command is just a mix of the `modelpreviewpitch` and `modelpreviewfov` commands, allows you to control the display of the preview itself in 3D context.

Note: `fov` can make the preview invisible at certain sizes and values (logically the same applies to `pitch` :P).

### `guicanvas.size w h`
This is the command that determines which screen model will be loaded and displayed, if a certain screen size is not available, the user will be prompted to generate it.

Alternatively you can generate screens with extra customizations using `guicanvas.genScreen`.

### `guicanvas name`
The `/guicanvas` command displays all .cfg files contained in the "guicanvas" folder and allows you to play or edit them.

![](https://github.com/SalatielSauer/misc/blob/master/guicanvas_raycast_1.gif) 
