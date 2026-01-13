# [`Textastic`](https://github.com/jimmy-zhening-luo/Textastic)

[ [Manual](https://www.textasticapp.com/v10/manual) ]

## `./`

### TextMate grammar: `${language}.tmBundle`

A language definition for Textastic and other text editors. Specifies:

- Language name
- File extensions
- Tokenization and grammar
- _Optional:_ Folding and indentation
- _Optional:_ Style

The language is uniquely identified by a scope, e.g., `source.ts` for TypeScript. The scope _should_ match a well-known TextMate scope as identified in [GitHub Linguist](https://github.com/github-linguist/linguist):

- [Languages](https://github.com/github-linguist/linguist/blob/main/lib/linguist/languages.yml) _([local](./language.yml))_
- [TextMate scopes](https://github.com/github-linguist/linguist/blob/main/grammars.yml) _([local](./language-scope.yml))_

#### Minimal implementation

At root (here), folder named `./${language}.tmBundle`, containing:

- Manifest: `./info.plist`
  - Guid
  - Language formal name, i.e. ${language}
  - Fake author (name and email)
  - _Optional:_ file source e.g.

- Syntax: `./Syntaxes/${language}.tmLanguage`
  - Guid
  - Scope name
  - File extensions
  - Grammar

#### ..._optional_

- Preference(s): `./Preferences/*.tmLanguage`
  - Comment pattern for folding
  - Indentation

- Theme: `Themes/${language}.tmTheme`
  - Non-standard scope-syntax mapping
  - Style
    - _Examples:_ [filmgirl/TextMate-Themes](https://github.com/filmgirl/TextMate-Themes)

### Template `./Templates/*.json`

Templates are shown when creating a new file. They prefill the filename/extension and insert a snippet into the new file content. Useful for adding frontmatter, footer, and other boilerplate.

The template content snippet definition support some subset of the TextMate snippet syntax.

#### Template Group

Each template file contains a grouped collection of templates (an empty collection or collection of one are both valid).

A new template can be added to an existing template file or by creating a new template file.

To create a new template file:

1. In Textastic, create New File.
1. In the new file creation UI, expand the template menu.
1. From the list of templates, select Template.

All templates belonging to a group show up under the same header in the template menu in the new fiLe UI.

Each template group file must be uniquely identified by a guid. When the template group file is created using the `Template` template in the new file UI, a new guid is automatically generated and placed into the new template group file.

### Code Completion: `./CodeCompletion/*.json`

A code completion file defines a mapping of scope to code completion triggers, suggestion text, and suggestion expansion for the given scope.

The scope is given as a TextMate scope, e.g., `(source.ts|source.js) - comment - string`.

Code Completions and Templates both use some subset of [TextMate snippet syntax](https://macromates.com/manual/en/snippets) ([_examples_](https://github.com/blach/Textastic-Customization)).

## Appendix

- [Unexpected behavior](https://feedback.textasticapp.com/communities/1/topics/1748-how-to-set-completion-file)
