# `comby -review` is broken for filepaths containing spaces
This repo demonstrates a bug in `comby`.

When running
```bash
comby Foo Bar .swift -review
```

from root of this repository, it fails with the error message:
```
Error attempting patch, command exited with 1.
Run the command again with DEBUG_COMBY=1 set in the environment for more info.
Press any key to continue, or exit now (Ctrl-C).
```

When running with `DEBUG_COMBY=1` as suggested the full log is:
```
Set custom external
Engine.Infer
<cl>Foo</cl>First for shift 0
Ok first'Extracted matched: Foo
Rule: (True)
Got back: true ""First for shift 29
Matches: 1 | Replacements: 1
There is 1 match in total, in 1 file to review.
Press any key to continue on this patching adventure (Ctrl-C to cancel).
------ src/foo bar/File.swift
++++++ src/foo bar/File.swift
@|-1,3 +1,3 ============================================================
 |import Foundation
 |
-|struct Foo {}
+|struct Bar {}
Accept change (y = yes [default], n = no, e = edit original, E = apply+edit, q = quit)?
y

[debug] File to patch: No file found--skip this patch? [y] 1 out of 1 hunks ignored--saving rejects to Oops.rej
,
Error attempting patch, command exited with 1.
Run the command again with DEBUG_COMBY=1 set in the environment for more info.
Press any key to continue, or exit now (Ctrl-C).
```

This error does not occur when using `-in-place` instead (i.e. running `comby Foo Bar .swift -in-place` works exactly as expected).
