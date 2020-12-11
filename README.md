# dynapage

Dynamically-loaded HTML pages

## Introduction

Third party-hosted CMSes can be quite disturbing sometimes, especially when updating existing pages requires a lot of efforts. This project allows users to load a relatively large page with only a 'stub'.

## Usage

### 1. Minified code for development

See [`dist/index.dist.html`](/dist/index.dist.html) for minified but editable skeleton code, or copy it from below:
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Dynapage for Distribution</title>
</head>

<body>
    <div hidden="" id="dynapage-config">
        <div id="dynapage-html-src" data-method="[HTTP METHOD TO YOUR PAGE]"
            data-source="[FILL YOUR HTML PAGE SOURCE HERE]"></div>
        <div id="dynapage-js-deps">
            <div data-source="[FILL YOUR JAVASCRIPT DEPENDENCY SOURCE 1 HERE]"></div>
            <div data-source="[FILL YOUR JAVASCRIPT DEPENDENCY SOURCE 2 HERE]" data-crossorigin="[CORS SETTINGS HERE]"
                data-integrity="[HASHES HERE]"></div>
            <!-- ... n more -->
        </div>
    </div>

    <div id="dynapage-container"></div>

    <script>var elemConfig=document.getElementById("dynapage-config");var elemSrc=document.querySelector("#dynapage-config > #dynapage-html-src");var pageSrc=elemSrc.dataset.source;var pageMeth=elemSrc.dataset.method;var htmlXhr=new XMLHttpRequest();htmlXhr.addEventListener("load",function(){if(htmlXhr.status===200){var elemContainer=document.getElementById("dynapage-container");var elemWrapper=document.createElement("div");elemWrapper.innerHTML=htmlXhr.responseText;elemContainer.insertAdjacentElement("beforeend",elemWrapper);var jsDeps=document.querySelectorAll("#dynapage-config > #dynapage-js-deps > div");for(var idx=0;idx<jsDeps.length;idx++){var dep=jsDeps[idx];var depDataset=dep.dataset;var elemJs=document.createElement("script");elemJs.setAttribute("src",depDataset.source);if(depDataset.hasOwnProperty("crossorigin")){elemJs.setAttribute("crossorigin",depDataset.crossorigin)}if(depDataset.hasOwnProperty("integrity")){elemJs.setAttribute("integrity",depDataset.integrity)}elemContainer.insertAdjacentElement("beforeend",elemJs)}}});htmlXhr.open(pageMeth,pageSrc);htmlXhr.send();</script>
</body>

</html>
```

### 2. Code for development without `<script>` tags

Sometimes it is not possible to directly insert `<script>` tags. The following version, as described in [`dist/index.noscript.dist.html`](/dist/index.noscript.dist.html), uses an invisible self-destroying `<button>` tag with `autofocus` property to escape most filters. The word `self-destroying` means that the button will be deleted once the script finishes loading.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Dynapage for Distribution</title>
</head>

<body>
    <div hidden="" id="dynapage-config">
        <div id="dynapage-html-src" data-method="[HTTP METHOD TO YOUR PAGE]"
            data-source="[FILL YOUR HTML PAGE SOURCE HERE]"></div>
        <div id="dynapage-js-deps">
            <div data-source="[FILL YOUR JAVASCRIPT DEPENDENCY SOURCE 1 HERE]"></div>
            <div data-source="[FILL YOUR JAVASCRIPT DEPENDENCY SOURCE 2 HERE]" data-crossorigin="[CORS SETTINGS HERE]"
                data-integrity="[HASHES HERE]"></div>
            <!-- ... n more -->
        </div>
    </div>

    <div id="dynapage-container"></div>

    <button style="position: absolute; top: 0; left: 0; height: 0; width: 0; padding: 0; margin: 0; border: 0;" id="b-m" autofocus="" onfocus="s=Function.call`${'Function\x28atob\x28\x27ZT1kb2N1bWVudC5nZXRFbGVtZW50QnlJZCgiYi1tIik7ZS5wYXJlbnROb2RlLnJlbW92ZUNoaWxkKGUpO3ZhciB0PWRvY3VtZW50LnF1ZXJ5U2VsZWN0b3IoIiNkeW5hcGFnZS1jb25maWcgPiAjZHluYXBhZ2UtaHRtbC1zcmMiKSxuPXQuZGF0YXNldC5zb3VyY2Uscj10LmRhdGFzZXQubWV0aG9kLG89bmV3IFhNTEh0dHBSZXF1ZXN0O28uYWRkRXZlbnRMaXN0ZW5lcigibG9hZCIsKGZ1bmN0aW9uKCl7aWYoMjAwPT09by5zdGF0dXMpe3ZhciBlPWRvY3VtZW50LmdldEVsZW1lbnRCeUlkKCJkeW5hcGFnZS1jb250YWluZXIiKSx0PWRvY3VtZW50LmNyZWF0ZUVsZW1lbnQoImRpdiIpO3QuaW5uZXJIVE1MPW8ucmVzcG9uc2VUZXh0LGUuaW5zZXJ0QWRqYWNlbnRFbGVtZW50KCJiZWZvcmVlbmQiLHQpO2Zvcih2YXIgbj1kb2N1bWVudC5xdWVyeVNlbGVjdG9yQWxsKCIjZHluYXBhZ2UtY29uZmlnID4gI2R5bmFwYWdlLWpzLWRlcHMgPiBkaXYiKSxyPTA7cjxuLmxlbmd0aDtyKyspe3ZhciBhPW5bcl0uZGF0YXNldCxkPWRvY3VtZW50LmNyZWF0ZUVsZW1lbnQoInNjcmlwdCIpO2Quc2V0QXR0cmlidXRlKCJzcmMiLGEuc291cmNlKSxhLmhhc093blByb3BlcnR5KCJjcm9zc29yaWdpbiIpJiZkLnNldEF0dHJpYnV0ZSgiY3Jvc3NvcmlnaW4iLGEuY3Jvc3NvcmlnaW4pLGEuaGFzT3duUHJvcGVydHkoImludGVncml0eSIpJiZkLnNldEF0dHJpYnV0ZSgiaW50ZWdyaXR5IixhLmludGVncml0eSksZS5pbnNlcnRBZGphY2VudEVsZW1lbnQoImJlZm9yZWVuZCIsZCl9fX0pKSxvLm9wZW4ocixuKSxvLnNlbmQoKQ==\x27\x29\x29\x28\x29'}`; s``"></button>

</body>

</html>
```

See [`examples/*`](/examples/) for usage notes and runnable code.
