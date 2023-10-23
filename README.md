# Tab jump out

Smart tab over is an Emacs minor mode that, when enabled, causes TAB to "jump over" closing
parentheses, braces, quotes, and some other punctuation.

I use Emacs' `electric-pair-mode` which means entering an open parenthesis causes the closing one
to be entered also.  When I finish typing the contents, the cursor is now inside the
parentheses and I want to move out.  With `electric-pair-mode`, the standard way is to type the
closing parenthesis which causes the cursor to move past it:

With this mode, pressing TAB will do the same thing.  It sounds small, and it is, but there is
something very pleasing about it for me.  Some of the closing characters require holding shift
or moving off the home row, but TAB is easy to hit.

The characters it will jump over are:

    } ] ) > : ; ` ' "

If you need to indent a line that starts with one of these characters, remember that Emacs'
will indent the entire line if you press TAB anywhere on the line in most programming modes.
If pressing TAB jumps over a character and you wanted to indent, just press TAB again.  In
modes that do not support this, you may need to toggle the mode off or use the spacebar.

# Installation

The tab-jump-out package is available on MELPA, so you can install with:


    M-x package-install [RET] smart-tab-over [RET]

   If you are using use-package, you can use this to enable globally:

   (use-package tab-jump-out
     :ensure t
     :config (tab-jump-out-global-mode 1))

If you want to install it only in some modes, don't enable global mode.  Add a hook to the
packages you want to use it in and call `(tab-jump-out-mode)`.

## With yasnippet

If you are using yasnippet, you may not want enable tab-jump-out-mode, but instead use the
fallback:

    (setq yas-fallback-behavior '(apply tab-jump-out 1))

This ensures yasnippet runs before tab-jump-out.
