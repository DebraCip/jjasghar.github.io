---
layout: post
title: "Changing fonts in emacs"
date: 2017-01-04 11:44:32
categories: emacs linux
---

Something I can never remember is how fonts are set in emacs. Here are some notes on how I figured it out.

First thing first, figure out what font you're using. Open up your `*scratch*` buffer and type:

```elisp
(face-attribute 'default :font)
```

In your minibuffer you should see the font name. I suggest moving over to the `*Messages*` buffer
yanking it and putting it in your `*scratch*` buffer with a `;` in front of it. (Notes are useful yeah?)

Lets set a default font now, take the following and eval it in your `*scratch*` buffer.

```elisp
(set-face-attribute 'default nil :font "-outline-Monaco-normal-normal-normal-mono-16-*-*-*-c-*-iso8859-1" )
```

Yay! You should have changed your font, to take from the [wiki][font_wiki] this "...change the default font for the current frame, as well as future frames..."

Now if you want to change the default font, but not the current frame, run the following:

```elisp
(set-face-attribute 'default t :font "-outline-Monaco-normal-normal-normal-mono-16-*-*-*-c-*-iso8859-1" )
```

After posting this to [reddit][reddit], [eli-zaretskii][eli] suggested using:

```elisp
(add-to-list 'default-frame-alist '(font . "your-font-name-here"))
```

Which works, but doesn't seem to update the current buffer. If you're testing out different fonts, personally, I'd like to see the effect without reloading.

If you haven't realized, the `16` is the font size in the line, personally `20` feels better, but you get the point. (eh? get it? eh? point?)

If you want to find other fonts, to play around with check out [here][font_list].

When you figure out what you want, you should add the `default nil` line to your `init.el` so every time you start emacs your font is configured.


[font_wiki]: https://www.emacswiki.org/emacs/SetFonts
[font_list]: https://www.emacswiki.org/emacs/GoodFonts
[reddit]: https://www.reddit.com/r/emacs/comments/5m0nig/notes_on_how_to_change_fonts_in_emacs_without/
[eli]: https://www.reddit.com/user/eli-zaretskii
