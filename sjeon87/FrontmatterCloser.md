---
name: Library/sjeon87/FrontmatterCloser
tags: meta/library
---

```space-lua
event.listen {
  name = 'editor.pageModified',
  run = function (e)
    local changes = e.data.changes[1]
    local inserted = changes.inserted
    if inserted ~= '-' then
      return 
    end
    local from = changes.newRange.from
    local to = changes.newRange.to
    if not ((from == 0 and to == 1) or (from == 1 and to == 2) or (from == 2 and to == 3)) then
      return
    end
    local text = editor.getText()
    local start_pos, end_pos = string.find(text, "^%-%-%-[ \t]*\n")
    if not start_pos then
      start_pos, end_pos = string.find(text, "^%-%-%-[ \t]*$")
    end
    if not start_pos then
      return
    end
    editor.insertAtPos("\n---", end_pos)
  end
}
```
