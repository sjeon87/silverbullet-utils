```space-lua
event.listen {
  name = "editor:pageLoaded",
  run = function(e)
    local currentPage = e.data[1]
    if not string.match(currentPage, "^%d%d%d%d%-%d%d%-%d%d$") then
      return
    end
    local journalPrefix = config.get("journal.prefix", "Journal/")
    local newPage = journalPrefix .. currentPage
    local text = editor.getText()
    space.writePage(newPage, text)
    editor.navigate(newPage, true)
    space.deletePage(currentPage)
  end
}
```
