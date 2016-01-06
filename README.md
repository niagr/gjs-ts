# gjs-ts
Typescript declarations for GNOME libraries compatible with GJS interpreter.

These declarations have been generated using [GIR2TS][GIR2TS].
They have NOT been tested yet. Do not use in production code.

## Status
Currently I'm testing it by using it to write an application. My aim is to submit this to DefinitelyTyped.

## Usage
The vast majority of the classes, interfaces, functions, unions, enums and bitfields are there. Sometimes, since the GObject property names are computed dynamically, methods, signals and properties often end up having the same names and interfaces overload inherited methods which doesn't fly with TypeScript. For this reason, certain classes, methods, etc. are ommited manually. These are commented out in the declaration files.

The important thing to remember is that you can escape the type system at any time by temporarily casting to ```any``` as shown below.
```typescript
(my_widget as any).anythingUnderTheSun();
```
We're Javascript programmers. We've seen uglier.

Also note that these declarations only describe the shape of existing JS bindings to C libraries. They do not provide any interop mechanism on their own. That is done by [GJS][GJS]. Therefore, we can't simply extend a GObject class or implement a GObject interface like we can a TypeScript class/interface. For that we have to use the ```lang.Class``` and ```lang.Interface``` functions. More information available here:
https://wiki.gnome.org/Projects/Gjs/StyleGuide#Classes
https://mail.gnome.org/archives/commits-list/2015-July/msg02569.html
https://bugzilla.gnome.org/show_bug.cgi?id=751343
http://stackoverflow.com/questions/22497990/lang-class-in-javascript
https://git.gnome.org/browse/gjs/tree/modules/lang.js

Also note that this only applies to GObject classes/interfaces. For your own TypeScript classes/interfaces you can keep using them the same way. How often do you really need inheritance anyway? o_0

[GIR2TS]: https://github.com/niagr/GIR2TS
[GJS]: https://wiki.gnome.org/Projects/Gjs

### Example
```typescript
import Gtk = imports.gi.Gtk;

declare let ARGV;
declare function print(msg: string);

(Gtk as any).init(null, 0);

let win = new Gtk.Window();

win.set_default_size(500, 500);

let button = new Gtk.Button();

button.set_label("my button");
win.add(button);

win.show_all();

Gtk.main();
```
