# xclip helper

I do a lot of json manipulation/reading in my day job. Often I need to copy
contents into the clipboard for putting into MR/Issues or documentation.

Today I finally automated that after years of typing `xclip -sel clipboard`

```shell
#!/usr/bin/env bash

if [ $# -gt 0 ]; then
  # read a file and pipe to xclip
  cat "$1" | xclip -sel clipboard
else
  # read from stdin; "text" | clip
  xclip -sel clipboard
fi
echo "copied to clipboard!"
```

Tags:

    #scripts #linux
