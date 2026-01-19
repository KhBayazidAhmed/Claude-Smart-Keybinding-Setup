

# VS Code / Cursor  Claude Smart Keybinding Setup

This guide will help you set up a **smart `Cmd+J` keybinding** in VS Code that:

* Opens the Claude sidebar if it’s closed
* Inserts at the cursor or selection (`claude-code.insertAtMentioned`)
* Toggles the auxiliary bar if the sidebar is open and no selection
* Works seamlessly with **one key** and avoids conflicts

---

## **1️⃣ Install the Multi-Command Extension**

1. Open VS Code.
2. Go to **Extensions** (`Cmd+Shift+X`).
3. Search for **`multi-command`** by `Ryuta46`.
4. Click **Install**.

> This extension allows running **multiple commands in sequence** from a single keybinding.

---

## **2️⃣ Configure Multi-Command Sequence**

1. Open **Settings (JSON)**:

   * Press `Cmd+,` → click the top-right `{}` icon to open `settings.json`.

2. Add the following at the bottom:

```jsonc
"multiCommand.commands": [
  {
    "command": "myCommands.openClaudeAndInsert",
    "sequence": [
      "workbench.view.extension.claude-sidebar", // Open Claude sidebar
      "claude-code.insertAtMentioned"            // Insert at cursor or selection
    ]
  }
]
```

> This ensures the sidebar opens first, then the insert command runs.

---

## **3️⃣ Update Keybindings**

1. Open **Keybindings JSON**:

   * Press `Cmd+Shift+P` → type **“Open Keyboard Shortcuts (JSON)”**.

2. Replace or add your keybindings with:

```jsonc
[
  // Cmd+J: Smart Claude command
  {
    "key": "cmd+j",
    "command": "extension.multiCommand.execute",
    "args": {
      "command": "myCommands.openClaudeAndInsert"
    }
  },
  // Toggle auxiliary bar if sidebar is visible AND no selection
  {
    "key": "cmd+j",
    "command": "workbench.action.toggleAuxiliaryBar",
    "when": "claudeVSCodeSidebar.visible && !editorHasSelection"
  },
  // Open Claude sidebar if auxiliary bar hidden AND no selection
  {
    "key": "cmd+j",
    "command": "workbench.view.extension.claude-sidebar",
    "when": "!auxiliaryBarVisible && !editorHasSelection"
  }
]
```

---

## **4️⃣ How to Use**

* Place your **cursor** or select text.
* Press **`Cmd+J`**.

Behavior:

1. **Sidebar closed + cursor/selection:** opens sidebar → inserts at cursor/selection.
2. **Sidebar open + selection:** inserts selection.
3. **Sidebar open + no selection:** toggles auxiliary bar.
4. Works **seamlessly with one keybinding**.

---

## **5️⃣ Notes**

* No conflicts with other shortcuts.
* You can change the keybinding from `Cmd+J` to any other key by editing `"key"`.
* Optional: Extend with more `multi-command` sequences for extra automation.

---

This setup makes **`Cmd+J` a single, smart shortcut** for working with Claude in VS Code. ✨



