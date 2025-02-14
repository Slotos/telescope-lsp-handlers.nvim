# telescope-lsp-handlers.nvim

## What

An extension for Telescope that registers handlers for
- `textDocument/declaration`
- `textDocument/definition`
- `textDocument/implementation`
- `textDocument/typeDefinition`
- `textDocument/references`
- `textDocument/documentSymbol`
- `workspace/symbol`
- `callHierarchy/incomingCalls`
- `callHierarchy/outgoingCalls`

## Why

Telescope's built-in LSP functions do not push items to the tagstack when picked manually, these handlers don't interfere with that process.

## How

Install this plugin with your favorite package manager and then load it:
```lua
require'telescope-lsp-handlers'.setup()
```

Then proceed to use the built-in API for supported requests.

### Customization
It is possible to customize handlers when calling setup. The following configuration is the default one:
```lua
require'telescope-lsp-handlers'.setup({
  declaration = {
    disabled = false,
    picker = { prompt_title = 'LSP Declarations' },
    no_results_message = 'Declaration not found',
  },
  definition = {
    disabled = false,
    picker = { prompt_title = 'LSP Definitions' },
    no_results_message = 'Definition not found',
  },
  implementation = {
    disabled = false,
    picker = { prompt_title = 'LSP Implementations' },
    no_results_message = 'Implementation not found',
  },
  type_definition = {
    disabled = false,
    picker = { prompt_title = 'LSP Type Definitions' },
    no_results_message = 'Type definition not found',
  },
  reference = {
    disabled = false,
    picker = { prompt_title = 'LSP References' },
    no_results_message = 'No references found'
  },
  document_symbol = {
    disabled = false,
    picker = { prompt_title = 'LSP Document Symbols' },
    no_results_message = 'No symbols found',
  },
  workspace_symbol = {
    disabled = false,
    picker = { prompt_title = 'LSP Workspace Symbols' },
    no_results_message = 'No symbols found',
  },
  incoming_calls = {
    disabled = false,
    picker = { prompt_title = 'LSP Incoming Calls' },
    no_results_message = 'No calls found',
  },
  outgoing_calls = {
    disabled = false,
    picker = { prompt_title = 'LSP Outgoing Calls' },
    no_results_message = 'No calls found',
  },
})
```
Note: setup can be performed multiple times, each new call will simply replace old handlers.

#### Keys explanation

- `disabled` indicates whether to disable a specific handler
- `no_results_message` provides a message emitted when no results had been found
- `picker` is an options table for telescope's `Picker:new` to be merged with this plugn defaults
  - `picker.entry` is a key that can be used to configure entry maker specifically (see `:h telescope.builtin.quickfix`), is removed before passing options to telescope

#### Applying themes to specific handler
```lua
require'telescope-lsp-handlers'.setup({
  reference = {
    picker = require('telescope.themes').get_dropdown({}), -- get_dropdown generates a table, which gets merged with plugin defaults
  },
}
```

#### Changing entry display
```lua
require'telescope-lsp-handlers'.setup({
  reference = {
    entry = {
      show_line = false, -- don't show matched code in picker list
    }
  },
}
```

```lua
require'telescope-lsp-handlers'.setup({
  reference = {
    entry = {
      trim_text = true, -- trim surrounding spaces from matched code
      fname_width = 50, -- increase space dedicated to filename to 50 from default 30
    }
  },
}
```

#### Disabling specific handlers
```lua
require'telescope-lsp-handlers'.setup({
  reference = {
    disabled = true,
  },
}
```
