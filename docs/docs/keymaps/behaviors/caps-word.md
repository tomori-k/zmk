---
title: Caps Word Behavior
sidebar_label: Caps Word
---

## Summary

The caps word behavior behaves similar to a caps lock, but will automatically deactivate when any key not in a continue list is pressed, or if the caps word key is pressed again. For smaller keyboards using [mod-taps](hold-tap.mdx#mod-tap), this can help avoid repeated alternating holds when typing words in all caps.

The modifiers are applied only to the alphabetic (`A` to `Z`) keycodes, to avoid automatically applying them to numeric values, etc.

### Behavior Binding

- Reference: `&caps_word`

Example:

```dts
&caps_word
```

### Configuration

#### Continue list

By default, the caps word will remain active when any alphanumeric character or underscore (`UNDERSCORE`), backspace (`BACKSPACE`), or delete (`DELETE`) characters are pressed. Any other non-modifier keycode sent will turn off caps word. If you would like to override this, you can set a new array of keys in the `continue-list` property in your keymap:

```dts
&caps_word {
    continue-list = <UNDERSCORE MINUS>;
};

/ {
    keymap {
        ...
    };
};
```

#### Applied modifier(s)

In addition, if you would like _multiple_ modifiers, instead of just `MOD_LSFT`, you can override the `mods` property:

```dts
&caps_word {
    mods = <(MOD_LSFT | MOD_LALT)>;
};

/ {
    keymap {
        ...
    };
};
```

### Auto activate with uppercase streak

You can enable an automatic activation of caps word after typing a streak of uppercase alphabetic keys. Set `auto-activate-upper-count` to the number of consecutive uppercase key presses required. A value of `0` keeps the feature disabled (default).

```dts
&caps_word {
    auto-activate-upper-count = <3>;
};
```

Only alphabetic keycodes (`A` to `Z`) are counted, and the press must include either left or right shift (implicit or explicit). Any non-uppercase alphabetic press resets the counter.

### Multiple Caps Breaks

If you want to use multiple caps breaks with different codes to break the caps, you can add additional caps words instances to use in your keymap:

```dts
/ {
    prog_caps: prog_caps {
        compatible = "zmk,behavior-caps-word";
        #binding-cells = <0>;
        continue-list = <UNDERSCORE>;
    };

    keymap {
        ...
    };
};
```
