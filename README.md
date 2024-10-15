# textAngularWithRtf v1.5.16

Fork of textAngular.
Added the ability to emit rtfcontent when using the ta-paste directive hook.

```html
<body>
  <div ng-app="app">
    <div ng-controller="TextEditController as textEdit">
      <text-angular
        name="pasteListener"
        ng-model="htmlVariable"
        ta-paste="modifyHtml($html, $textFormat, $rtfContent)"
        ta-text-editor-class="border border:2 border-color:gold-60"
        ta-html-editor-class="border border:2 border-color:gold-60"
      ></text-angular>
    </div>
  </div>

  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/gh/tno2007/textAngularWithRtf@latest/dist/textAngular.css"
  />
  <!-- pull fontawesome to show editor icons -->
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.6.0/css/all.min.css"
    integrity="sha512-Kc323vGBEqzTmouAECnVceyQqyqdsSiqLQISBL29aUW4U/M7pSPA/gEUZQqv1cwx4OnYxTxve5UMg5GT6L4JJg=="
    crossorigin="anonymous"
    referrerpolicy="no-referrer"
  />

  <!-- include needed libraries -->
  <script src="https://cdn.jsdelivr.net/gh/tno2007/textAngularWithRtf@latest/dist/textAngular-rangy.min.js"></script>
  <script src="https://cdn.jsdelivr.net/gh/tno2007/textAngularWithRtf@latest/dist/textAngular-sanitize.min.js"></script>
  <script src="https://cdn.jsdelivr.net/gh/tno2007/textAngularWithRtf@latest/dist/textAngular.min.js"></script>

  <!-- lib to convert rtf to html to support this example -->
  <script src="https://cdn.jsdelivr.net/gh/tno2007/docx-cleaner-es5@latest/dist/cleandocx.umd.js"></script>

  <script>
    angular
      .module("app", ["textAngular"])
      .controller("TextEditController", function ($scope) {
        $scope.htmlVariable = "";
        $scope.message = "Hello textAngular!";

        $scope.modifyHtml = function ($html, $textFormat, $rtfContent) {
          // test to see if rtf content was pasted
          if ($textFormat === "text/rtf") {
            // do something with $rtfContent here...
            // eg. convet rtfcotent to html, preserving images
            const cleanHtml = cleanDocx.cleanDocx($html, $rtfContent);
            // return altered paste content back to textAngular
            return cleanHtml;
          } else {
            // return passed in html back to textAngular
            return $html;
          }
        };
      });
  </script>
</body>
```


# Changelog

## 14 October 2024
## v1.5.19

Added console log for when bullet-list issue occurs

## 14 October 2024
## v1.5.18

Fix bullet list copy-paste issue

