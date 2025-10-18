# tab-jump-out

[![MELPA](https://melpa.org/packages/tab-jump-out-badge.svg)](https://melpa.org/#/tab-jump-out)

**tab-jump-out** is a small Emacs minor mode that makes the `TAB` key “jump out” of closing
parentheses, braces, quotes, and similar punctuation.

`tab-jump-out` is simple but satisfying — once you start using it, `TAB` will feel like the
natural way to step out of parentheses and quotes.

## Overview

When using Emacs’ built-in `electric-pair-mode`, typing an opening parenthesis automatically inserts
the matching closing one, leaving the cursor inside the pair. Normally, you would type the closing
character again to move past it:

    (|) → ()|

With **tab-jump-out** enabled, pressing `TAB` performs that jump for you — no need to reach for
Shift or move off the home row. It’s a small change, but one that feels very natural once you try
it.

By default, `TAB` will jump over any of these characters:

    } ] ) > : ; ` ' "

This can be configured with the `tab-jump-out-delimiters` variable.  The variable is
[buffer-local](https://www.gnu.org/software/emacs/manual/html_node/elisp/Buffer_002dLocal-Variables.html)
so it can have different values for different modes.

### Indentation behavior

If you need to indent a line that starts with one of these characters, remember that Emacs'
will indent the entire line if you press TAB anywhere on the line in most programming modes.
If pressing TAB jumps over a character and you wanted to indent, just press TAB again.

In modes that don’t support indentation with `TAB`, you can temporarily disable
`tab-jump-out-mode`, use the spacebar to adjust alignment manually, or use rigid-indent-mode
(C-x TAB).

## Installation

The package is available on [MELPA](https://melpa.org/), so you can install it with:

    M-x package-install [RET] tab-jump-out [RET]

If you are using `use-package`, you can use this to enable globally:

``` elisp
(use-package tab-jump-out
  :ensure t
  :config 
  (tab-jump-out-global-mode 1))
```

If you only want it enabled in certain modes, don’t enable global mode.
Instead, add a hook to those modes:

``` elisp
(add-hook 'python-mode-hook #'tab-jump-out-mode)
```

You can also do this in use-package with the `:hooks` keyword.

## Interaction with ya-snippet

When editing a snippet template, `TAB` is used to jump between snippet fields.  If the
character following a field is one `tab-jump-out` would normally jump over, it does so and will
exit snippet editing early.  

For example, consider a Python snippet like:

    def {1:function_name}({2:args}):
        {0}

In this case, you can temporarily disable tab-jump-out while expanding snippets:

``` elisp
(add-hook 'yas-before-expand-snippet-hook 
          (lambda() (tab-jump-out-mode -1)))
(add-hook 'yas-after-exit-snippet-hook 
          (lambda() (tab-jump-out-mode 1)))
```


This unconditionally re-enables the mode afterward.  If you don't use it globally or sometimes
disable it manually, track its prior state in a local variable and re-enable it only if it was
previously active.

## License

tab-jump-out is distributed under the MIT License.
See the LICENSE file for details.
