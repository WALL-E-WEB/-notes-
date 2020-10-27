vscode 配置自动格式化

需要的vscode插件：

- vetur+eslint

setting配置：

```json
"editor.tabSize": 2,
    "files.associations": {
        "*.vue": "vue"
    },
    "eslint.autoFixOnSave": true,
    "eslint.options": {
        "extensions": [
            ".js",
            ".vue"
        ]
    },
    "eslint.validate": [
        "javascript",
        {
            "language": "vue",
            "autoFix": true
        },
        "html",
        "vue"
    ],
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
        "**/dist": true
    },
    "emmet.syntaxProfiles": {
        "javascript": "jsx",
        "vue": "html",
        "vue-html": "html"
    },
    "git.confirmSync": false,
    "window.zoomLevel": -1,
    "editor.renderWhitespace": "boundary",
    "editor.cursorBlinking": "smooth",
    "editor.minimap.enabled": true,
    "editor.minimap.renderCharacters": false,
    "editor.fontFamily": "'Droid Sans Mono', 'Courier New', monospace, 'Droid Sans Fallback'",
    "window.title": "${dirty}${activeEditorMedium}${separator}${rootName}",
    "editor.codeLens": true,
    "editor.snippetSuggestions": "top",
    "eslint.migration.2_x": "off",
    "vetur.format.defaultFormatterOptions": {
        "prettier": {
          // Prettier option here
          "semi": false,
          "singleQuote": true,
          "trailingComma": "none"
        }
    },
```

