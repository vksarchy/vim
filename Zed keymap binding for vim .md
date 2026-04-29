[
  // ─── VimControl: normal + visual + operator ───────────────────
  {
    "context": "VimControl && !menu",
    "bindings": {
      "n": "editor::MoveDown",
      "e": "editor::MoveUp",
      "i": "editor::MoveRight",
      "h": "editor::MoveLeft",

      "k":         ["vim::NextWordEnd", { "ignore_punctuation": false }],
      "shift-k":   ["vim::NextWordEnd", { "ignore_punctuation": true }],
      "g k":       "vim::PreviousWordEnd",
      "g shift-k": ["vim::PreviousWordEnd", { "ignore_punctuation": true }],

      "l":       "vim::MoveToNextMatch",
      "shift-l": "vim::MoveToPreviousMatch",

      "shift-n": ["editor::MoveDownByLines", { "lines": 5 }],
      "shift-e": ["editor::MoveUpByLines", { "lines": 5 }]
    }
  },

  // ─── Visual mode: override movement to extend selection ───────
  {
    "context": "Editor && vim_mode == visual && !menu",
    "bindings": {
      "n": "editor::SelectDown",
      "e": "editor::SelectUp",
      "i": "editor::SelectRight",
      "h": "editor::SelectLeft",

      "shift-n": ["editor::SelectDownByLines", { "lines": 5 }],
      "shift-e": ["editor::SelectUpByLines", { "lines": 5 }],

      // Move selected lines up/down
      "alt-n": "editor::MoveLineDown",
      "alt-e": "editor::MoveLineUp"
    }
  },

  // ─── Normal mode only ─────────────────────────────────────────
  {
    "context": "Editor && vim_mode == normal && !menu",
    "bindings": {
      "j": "vim::JoinLines",

      "space i":       ["workspace::SendKeystrokes", "i"],
      "space shift-i": ["workspace::SendKeystrokes", "shift-i"],

      ";": "command_palette::Toggle",

      "space w": "workspace::Save",
      "space e": "file_finder::Toggle",
      "space r": "projects::OpenRecent",
      "space x": "pane::CloseActiveItem",

      "space l": "pane::ActivateNextItem",
      "space h": "pane::ActivatePreviousItem",
      "space b": "tab_switcher::Toggle",
      "space q": "pane::CloseActiveItem",

      "space f f": "file_finder::Toggle",
      "space f g": "workspace::NewSearch",
      "space f b": "tab_switcher::Toggle",
      "space /":   "buffer_search::Deploy",

      "space v": "pane::SplitRight",
      "space s": "pane::SplitDown",

      "ctrl-d": ["workspace::SendKeystrokes", "ctrl-d z z"],
      "ctrl-u": ["workspace::SendKeystrokes", "ctrl-u z z"],

      "space z": "workspace::ToggleCenteredLayout",

      "escape": "vim::ClearOperators"
    }
  },

  // ─── Insert mode ──────────────────────────────────────────────
  {
    "context": "Editor && vim_mode == insert",
    "bindings": {
      "t n": "vim::NormalBefore"
    }
  }
]
