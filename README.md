# PrettySharp for Emacs

`prettysharp` is a function that formats the current buffer by running the PrettySharp formatter.
We also expose a minor mode (`prettysharp-mode`) that formats the current buffer on save.

## Configuration

### The Basics

Ensure that the prettysharp program is installed:

```
which prettysharp
```

If you don't have it, you can figure out how to install it with instructions in the [repository for PrettySharp](https://github.com/DeCarabas/PrettySharp).

If you *do* have it, but it's not on your path, or you just want to use some different version, you can customize the `prettysharp-command` variable.

Once it's installed properly, you can require the package with:

```
(require 'prettysharp)
```

Presumably then you'd want to set it up to automatically format on save, so attach it to `csharp-mode` like:

```
(add-hook 'csharp-mode-hook 'prettysharp-mode)
```

You can also just run it manually (like an animal) with `M-x prettysharp`.
But why wouldn't you put it in your save hook?
What are you, some kind of horrible savage?
We're trying to have a civilized programming language here, people!

### Showing Errors

PrettySharp will only format buffers that it can parse: if something goes wrong during parsing it leaves the buffer alone.
If you find yourself frequently confused by why it's not formatting your buffer, you can customize the `prettysharp-show-errors` variable.
In the long tradition laid down by such commands as gofmt and prettier, this variable can be set to display errors in its own buffer ('buffer'), or in the echo area ('echo').

Note that if you're running prettysharp as a save hook (and again, why wouldn't you?) emacs is probably going to echo more stuff as part of saving the file.
As a result, your error messages are not going to be visible in the echo area.

Also, PrettySharp is generally pretty stingy about error recovery, and will probably only show the first error it finds.
You're probably better off using omnisharp or flycheck or some other error detection mode to find and fix all your parsing errors.
