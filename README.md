# NAME

lemonbar - Featherweight lemon-scented bar

<img src="https://github.com/LemonBoy/bar/workflows/Does%20this%20build%20look%20infected%3F/badge.svg">

# SYNOPSIS

*lemonbar* [-h | -g *width***x***height***+***x***+***y* | -o | -b | -d | -f *font* | -p | -n *name* | -u *pixel* | -B *color* | -F *color* | -U *color*]

# DESCRIPTION

**lemonbar** (formerly known as **bar**) is a lightweight statusbar based on XCB.
Provides full UTF-8 support, basic formatting, RandR and Xinerama support and
EWMH compliance without wasting your precious memory.

# INPUT

The data to be parsed is read from the standard input, parsing and printing the
input data are delayed until a newline is found.

# OPTIONS

* **-h**

    Display the help and exit.

* **-g** *width***x***height***+***x***+***y*

    Set the window geometry. If a parameter is omitted it's filled with the default value. If the *y* parameter is specified along with the **-b** switch then the position is relative to the bottom of the screen.

* **-o** *name*

    Set next output to *name*. May be used multiple times; order is significant. If any **-o** options are given, only **-o** specified monitors will be used. Invalid output names are silently ignored. (only supported on randr configurations at this time)

* **-b**

    Dock the bar at the bottom of the screen.

* **-d**

    Force docking without asking the window manager. This is needed if the window manager isn't EWMH compliant.

* **-f** *font*

    Specifies a font to use. Can be used multiple times to load more than a single
    font.

* **-p**

    Make the bar permanent, don't exit after the standard input is closed.

* **-n** *name*

    Set the WM_NAME atom value for the bar.

* **-u** *pixel*

    Sets the underline width in pixels. The default is 1.

* **-B** *color*

    Set the background color of the bar. *color* must be specified in the hex format (#aarrggbb, #rrggbb, #rgb). If no compositor such as compton or xcompmgr is running the alpha channel is silently ignored.

* **-F** *color*

    Set the foreground color of the bar. Accepts the same color formats as **-B**.

* **-U** *color*

    Set the underline color of the bar. Accepts the same color formats as **-B**.

# FORMATTING

lemonbar provides a screenrc-inspired formatting syntax to allow full customization at runtime. Every formatting block is opened with `%{{` and closed by `}` and accepts the following commands, the parser tries its best to handle malformed input. Use `%%` to get a literal percent sign (`%`).

* **R**

    Swap the current background and foreground colors.

* **l**

    Aligns the following text to the left side of the screen.

* **c**

    Aligns the following text to the center of the screen.

* **r**

    Aligns the following text to the right side of the screen.

* **O***width*

    Offset the current position by *width* pixels in the alignment direction.

* **B***color*

    Set the text background color. The parameter *color* can be *-* or a color in one of the formats mentioned before. The special value *-* resets the color to the default one.

* **F***color*

    Set the text foreground color. The parameter *color* can be *-* or a color in one of the formats mentioned before. The special value *-* resets the color to the default one.

* **T***index*

    Set the font used to draw the following text. The parameter *index* can either be *-* or the 1-based index of the slot which contains the desired font. If the parameter is *-* lemonbar resets to the normal behavior (matching the first font that can be used for the character). If the selected font can't be used to draw a character, lemonbar will fall back to normal behavior for that character

* **U***color*

    Set the text underline color. The parameter *color* can be *-* or a color in one of the formats mentioned before. The special value *-* resets the color to the default one.

* **A***button*:*command*:

    Create a clickable area starting from the current position, when the area is clicked *command* is printed on stdout. The area is closed when a **A** token, not followed by : is encountered.

    Eg. *%{A:reboot:} Click here to reboot %{A}*

    The *button* field is optional, it defaults to the left button, and it's a number ranging from 1 to 5 which maps to the left, middle, right, scroll up and scroll down movements. Your mileage may vary.

    Nested clickable areas can trigger different commands.

    Eg. *%{A:reboot:}%{A3:halt:} Left click to reboot, right click to shutdown %{A}%{A}*

* **S***dir*

    Change the monitor the bar is rendered to. *dir* can be either

    * **+**/**-**

        Next/previous monitor.

    * **f**/**l**

        First/last monitor.

    * *0-9*

        Nth monitor.

    * *n***NAME**

        Named monitor.
        Eg. *%{SnHDMI-0} This text will show up on the HDMI-0 output*

**Attribute modifiers**

* **+***attribute*

    Set the attribute *attribute* for the following text.

* **-***attribute*

    Unset the attribute *attribute* for the following text.

* **!***attribute*

    Toggle the attribute *attribute* for the following text.

Where *attribute* is one of the following

* **o**

    Draw a line over the text.

* **u**

    Draw a line under the text.

# OUTPUT

Clicking on an area makes lemonbar output the command to stdout, followed by a newline, allowing the user to pipe it into a script, execute it or simply ignore it. Simple and powerful, that's it.

# WWW

[git repository](https://github.com/LemonBoy/bar)

# AUTHOR

2012-2020 (C) The Lemon Man

Xinerama support was kindly contributed by Stebalien

RandR support was kindly contributed by jvvv

Clickable areas support was heavily based off u-ra contribution
