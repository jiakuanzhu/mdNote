# paredit
 paredit.el --- minor mode for editing parentheses  -*- Mode: Emacs-Lisp -*-

## Installation
 Install paredit by placing `paredit.el' in `/path/to/elisp', a
 directory of your choice, and adding to your .emacs file:
```
   (add-to-list 'load-path "/path/to/elisp")
   (autoload 'enable-paredit-mode "paredit"
     "Turn on pseudo-structural editing of Lisp code."
     t)
```
## Start to use Paredit
 Start Paredit Mode on the fly with `M-x enable-paredit-mode RET',
 or always enable it in a major mode `M' (e.g., `lisp') with:
```
   (add-hook 'M-mode-hook 'enable-paredit-mode)
```
## Customization
 Customize paredit using `eval-after-load':
```
   (eval-after-load 'paredit
     '(progn
        (define-key paredit-mode-map (kbd "ESC M-A-C-s-)")
          'paredit-dwim)))
```
## Key binding

### Delimiter
-` )`:  移出()
- `"`: 在引用内，加转意字符\" 
- ;;abcd... 正常输入
- 强制加入：加`C-q`，正常输入，为补全"

## M-( & M-"
将单字或者选中几个字加() ""

### Kill
- `C-k` 删到()，
- `C-d` 删不掉单独的( ) ""，首先用C-k清空内容后才能删除
- 强制删除：`C-u C-d`，或者`C-u C-k`



## C-<right>
(foo (bar | baz) quux)  
(foo (bar | baz quux))
将list中最后sexp移出

C-<left>
将list中后面临近sexp移入

## Slurping and Barfing
Slurping is when the current S-expression or string is expanded by pulling in the next outer S-expression. Barfing is the opposite, contracting the S-expression by pushing out it's last-most form.

Slurping is provided by paredit-forward-slurp-sexp, bound to `C-)`, and barfing is provided by paredit-forward-barf-sexp that is bound to `C-}`.
Slurp and barf backwards with paredit-backward-slurp-sexp, bound to `C-(`, and paredit-backward-barf-sexp, bound to `C-{`.

Slurp:drink or eat with a loud sucking noise
Barf:an attack of vomiting.
## Structural Navigation
Paredit provides functions for graceful S-expression navigation, allowing you to move forward and backward amongst siblings, raise up to the enclosing S-expression and descend back down into the children.

Move forward and backward inside an S-expression using paredit-forward and paredit-backward, bound to `C-M-f` and `C-M-b` respectively. Upon reaching a delimiter, a further invocation will move the cursor outside of the current S-expression and into the enclosing S-expression.

To descend forwards use paredit-forward-down, bound to `C-M-d`. To reverse that and ascend backwards use paredit-backward-up, bound to `C-M-u`.
Then, when you want to descend backward you can use paredit-backward-down, bound to `C-M-p`. And to reverse that and ascend forwards use paredit-forward-up, bound to `C-M-n`.

## Splicing
Splicing is the act of removing the current S-expression and joining (some of) the contents with the enclosing S-expression. There are two splices that will kill the content of the current S-expression either to the front of rear of the cursor.

Kill backwards with paredit-splice-sexp-killing-backward, bound to `M-<up>`.
And kill forwards with paredit-splice-sexp-killing-forward that is bound to `M-<down>`.
And there is a no kill variant paredit-splice-sexp bound to M-s, shown here splicing the quotes off a string.

## Splitting and Joining
An S-expression can be split into two, and two S-expressions can be joining back together into one.
Split is paredit-split-sexp and bound to `M-S`, join is paredit-join-sexps and bound to `M-J`. Note that the S and J are both uppercase.

