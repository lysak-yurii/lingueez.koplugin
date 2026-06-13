# Troubleshooting Dictionary Sync Plugin

## Plugin Not Appearing in Menu or Word Selection

If the plugin shows up in Plugin Management but doesn't appear in the menu or word selection, try these steps:

### 1. Verify Plugin is Enabled
- Go to **Settings** → **Plugin Management**
- Find "Dictionary Sync" in the list
- Make sure it's **enabled** (toggle should be ON)

### 2. Restart KOReader
- Close KOReader completely
- Reopen KOReader
- Open a document (the plugin only works when a document is open)

### 3. Check Plugin Location
The plugin should be in:
- **Android**: `/sdcard/koreader/plugins/dictionary-sync.koplugin/`
- **Linux**: `~/.config/koreader/plugins/dictionary-sync.koplugin/`
- **Windows**: Check KOReader settings for plugin directory

The folder must be named exactly `dictionary-sync.koplugin` (with the `.koplugin` extension)

### 4. Verify Files Exist
Make sure these files exist in the plugin folder:
- `_meta.lua`
- `main.lua`

### 5. Check KOReader Logs
- Look for "Dictionary Sync" messages in KOReader logs
- Logs location varies by platform:
  - **Android**: Check logcat or KOReader log file
  - **Linux**: `~/.config/koreader/koreader.log`
  - **Windows**: Check KOReader installation directory for log files

Look for these messages:
- "Dictionary Sync: init() called"
- "Dictionary Sync: Menu registered"
- "Dictionary Sync: Highlight dialog button added"
- "Dictionary Sync plugin initialized successfully"

If you see error messages, note them down.

### 6. Test in Document Context
- The plugin only works when a document is open
- Open any book/document in KOReader
- Try accessing the menu: **Menu** → **Dictionary Sync**
- Try selecting a word - you should see "Save to Dictionary" in the popup

### 7. Manual Menu Check
- Open a document
- Go to **Menu** → Look for **Dictionary Sync** under the **Tools** section
- If it's not there, the plugin may not be initializing correctly

### 8. Reinstall Plugin
If nothing works:
1. Disable the plugin in Plugin Management
2. Delete the `dictionary-sync.koplugin` folder
3. Copy it again to the plugins directory
4. Restart KOReader
5. Enable the plugin
6. Open a document and test

## Common Issues

### "No UI context available" in logs
- This means the plugin is trying to initialize outside of a document
- Open a document first, then the plugin will initialize

### Menu appears but word selection doesn't
- Make sure you're selecting text (long-press or word selection)
- The "Save to Dictionary" button should appear in the highlight popup menu
- If it doesn't appear, check logs for "Highlight dialog button added" message

### Plugin crashes KOReader
- Check for syntax errors in `main.lua`
- Make sure all required modules are available
- Check KOReader version compatibility

## Still Not Working?

If the plugin still doesn't appear after trying all these steps:
1. Check KOReader version (plugin may require a specific version)
2. Verify the plugin structure matches exactly the assistant.koplugin example
3. Check for any error messages in KOReader logs
4. Try disabling other plugins to rule out conflicts

