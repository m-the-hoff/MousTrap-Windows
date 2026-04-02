# MousTrap Windows v1.2

A Macintosh-like windowing toolkit for the Apple //e, written entirely in 6502 assembly using the Merlin assembler. Created in 1987.

The entire toolkit fits in **under 8KB of code** with 2KB of tables — providing a full GUI environment with windows, menus, scroll bars, buttons, mouse support, and more on stock Apple //e hardware.

## Features

- Up to 255 windows (dialog or document, with optional accessories)
- Scroll bars with automatic tracking, thumb dragging, paging, and arrow events
- Window dragging, resizing, and close box
- Pull-down menus with disabled/checked items, dividers, and keyboard shortcuts
- Control items: buttons, static text, scroll bars, rectangles
- Drawing with any 8x8 bit pattern, AND/OR/EOR/STORE modes, automatic clipping
- Text rendering with any MultiScribe font
- Input from mouse, keyboard, or joystick (with adjustable response and speedup card support)
- Single or double hi-res mode, switchable at any time
- Built-in 16-bit CPU emulator (30 instructions, modeled after the 68000)
- High-speed 3D line drawing algorithms

## Running the Demo

A pre-built bootable ProDOS disk image (`MousTrap_Demo.dsk`) is included with everything needed to run the demo.

### Option 1: Scullin Steel Web Emulator (No Install Required)

1. Go to [Apple //e JS](https://www.scullinsteel.com/apple//e)
2. Click the **floppy disk icon** next to "Disk 1"
3. Select `MousTrap_Demo.dsk` from your local machine
4. The disk will boot ProDOS and launch the MousTrap demo automatically

### Option 2: microM8 (macOS)

Install via Homebrew:

```bash
brew tap lifepillar/appleii
brew install --cask lifepillar/appleii/microm8
```

On first run you may need to clear the Gatekeeper quarantine:

```bash
xattr -dr com.apple.quarantine /Applications/microM8.app
```

Launch with the demo disk:

```bash
/Applications/microM8.app/Contents/MacOS/microM8 \
  -profile apple2e-en \
  -drive1 MousTrap_Demo.dsk
```

## Project Structure

```
MousTrap Windows 1.2/       Main toolkit source and compiled binaries
  ├── MTW.S                  Main toolkit code
  ├── MTW.4000               Compiled toolkit (8KB, loads at $4000)
  ├── MTW.MACROS.S           Macro definitions
  ├── MTW.EQUATE.S           Equate definitions
  ├── MTWMENUS.S             Menu handling
  ├── DOMOUSE.S              Mouse/input event handler
  ├── WDWDRAW.S              Window drawing
  ├── DRAWRECT.S             Rectangle drawing
  ├── CURSOR.S               Cursor management
  ├── OPENWDW.S / CLOSEWDW.S / SIZEIT.S
  ├── ...                    (additional toolkit modules)
  └── DEMO/                  Complete demo application
      ├── DEMO.SYSTEM         ProDOS boot loader
      ├── DEMO                Compiled demo binary
      ├── DEMO3D.S / D3D.S   3D graphics routines
      ├── SHAPES.S            Shape drawing
      ├── DRAWCIRCLE.S        Circle drawing
      └── ...                 (fonts, patterns, shape tables)

Merlin versions/            Merlin assembler disk images (DOS 3.3)
WORKDSK1/ WORKDSK2/         Working copies of source files
Source Text listings/        Human-readable source listings
MousTrap_Demo.dsk           Bootable ProDOS demo disk image
```

The `.S` files are in Merlin assembler's tokenized binary format. Readable source text listings for select modules are in the `Source Text listings/` directory.

## Building from Source

The source was developed using the Merlin Pro assembler running natively on Apple //e hardware. Several versions of the Merlin assembler are included as DOS 3.3 disk images in `Merlin versions/`.

## License

Copyright (c) 1985-1989 Michael Hoffman / Micronics. Released under the [MIT License](LICENSE).
