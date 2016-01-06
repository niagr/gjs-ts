# gjs-ts
Typescript declarations for GNOME libraries compatible with GJS interpreter.

## Example
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
