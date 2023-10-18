# $ python -m http.server --bind 127.0.0.1 8080

```html
<!DOCTYPE html>
<html>
  <head>
      <meta http-equiv="Content-Type" content="text/html;charset=utf-8" />
      <link
          rel="stylesheet"
          data-name="vs/editor/editor.main"
          href="./min/vs/editor/editor.main.css"
      />
  </head>
  <body>

      <div id="container" style="overflow: hidden; width: 100%; height: 100%; position: absolute"></div>

      <script>
          var require = { paths: { vs: './min/vs' } };
      </script>
      <script src="./min/vs/loader.js"></script>
      <script src="./min/vs/editor/editor.main.nls.js"></script>
      <script src="./min/vs/editor/editor.main.js"></script>

      <script>
          const urlParams = new URLSearchParams(window.location.search);

          for (const [key, value] of urlParams) {
              console.log(`${key}=${value}`);
          }


          let fileContent = null;


          fetch(urlParams.get("context"))
              .then(response => response.text())
              .then(content => {
                  // Save the content to the variable
                  fileContent = content;
              })
              .catch(error => {
                  console.error(`Error fetching and saving content: ${error}`);
              });


          var editor = monaco.editor.create(document.getElementById('container'), {
              value: `${fileContent}`,
              language: `${urlParams.get("lang")}`,
              lineNumbers: `${urlParams.get("lineNumbers")}`,
              theme: `${urlParams.get("theme")}`,
              minimap: `${urlParams.get("minimap")}`,
              background: `${urlParams.get("background")}`,
              folding: `${urlParams.get("folding")}`,
              javascriptDefaults: `${urlParams.get("javascriptDefaults")}`,
              typescriptDefaults: `${urlParams.get("typescriptDefaults")}`,
              javascriptDefaultsNoSemanticValidation: `${urlParams.get("javascriptDefaultsNoSemanticValidation")}`,
              typescriptDefaultsNoSemanticValidation: `${urlParams.get("typescriptDefaultsNoSemanticValidation")}`,
              javascriptDefaultsNoSyntaxValidation: `${urlParams.get("javascriptDefaultsNoSyntaxValidation")}`,
              typescriptDefaultsNoSyntaxValidation: `${urlParams.get("typescriptDefaultsNoSyntaxValidation")}`,
              automaticLayout: true,
          });
      </script>
  </body>
</html>

```


# Obsidian Code Files

> Plugin for ObsidianMD to show and edit code files along other notes.

The plugin adds a code editor view to Obsidian. The code editor uses the powerful
[Monaco Editor](https://microsoft.github.io/monaco-editor/), which also powers VS Code.

*__🚀 New Feature: The plugin now also supports editing individual code blocks from Markdown
files in an embedded Monaco Editor instance. Read [below](#new-feature-code-block-editing).__*

**Caveat: This plugin currently relies on hosted dependencies and thus needs an internet connection.
Read [below](#caveat-online-dependency) for more information.**

In the plugin settings, you can configure for which file extensions the editor will be
available as default editor. You can also create new code files, either by right clicking
on a folder in the side pane and clicking on "Create Code File", search for
"Create new Code File" in the command palette or by using the "Create Code File" button
in the ribbon.

![img_1.png](img_1.png)

## New Feature: Code Block Editing

As of Version 1.1.0, the plugin also supports editing individual code blocks from any
Markdown document in the editor. You
can either invoke the command palette and search for "Open Current Code Block in Monaco
Editor", or right click on any code block and click on "Edit Code Block in Monaco Editor".

This will open a new modal with a Monaco Editor instance in which you can edit the code
block, which will automatically sync back to the block in your document when you close
the modal.

![fence-editing.gif](fence-editing.gif)

## New Feature: Allows editing CSS Snippets

Search for the command "Edit CSS Snippet" to search CSS Snippets that exist in your
Obsidian vault and edit them in the Monaco Editor.

![css-files.gif](css-files.gif)

## More Screenshots

![img_2.png](img_2.png)

![img.png](img.png)

## Caveat: Online dependency

Due to the complicated nature of bundling the Monaco Editor, the plugin currently relies on
a hosted version of the editor. This means that the plugin needs an internet connection to
work, and has a dependency on the hosted editor, which is currently available on
https://embeddable-monaco.lukasbach.com.

I hope to remove this dependency in the future, but this was the easiest way to get the
plugin to work for now.
