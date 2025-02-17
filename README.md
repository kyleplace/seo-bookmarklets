# SEO Bookmarklets for Google Chrome

## highlight no follow links	
`
javascript:(function() {
    var links = document.getElementsByTagName('a');
    for (var i = 0; i < links.length; i++) {
        if (links[i].rel.includes('nofollow')) {
            links[i].style.backgroundColor = 'yellow';
        }
    }
})();
`
## highlight htags	
`
javascript:(function() {   var hTags = document.querySelectorAll("h1, h2, h3, h4, h5, h6");   for (var i = 0; i < hTags.length; i++) {     hTags[i].style.backgroundColor = "lightgreen";   } })();
`
## Extract h tags to new tab
`
javascript:(function() {  var hTags = document.querySelectorAll("h1, h2, h3, h4, h5, h6");  var div = document.createElement("div");  div.innerHTML = "";  for (var i = 0; i < hTags.length; i++) {    var hTag = hTags[i];    var text = hTag.textContent;    var level = hTag.tagName.charAt(1) - 1;    var span = document.createElement("span");    span.innerHTML = text;    span.style.paddingLeft = level * 20 + "px";    div.appendChild(span);    div.innerHTML += "<br>";  }  var newTab = window.open("about:blank");  newTab.document.body.appendChild(div);})()
`

## Show image alt text and dimensions
`
javascript:(function(){  var images = document.querySelectorAll("img");  for (var i = 0; i < images.length; i++) {    var image = images[i];    var altText = image.getAttribute("alt");    var dimensions = image.naturalWidth + "x" + image.naturalHeight;    var div = document.createElement("div");    div.textContent = altText + " | " + dimensions;    div.style.backgroundColor = "lightgreen";    image.parentNode.insertBefore(div, image.nextSibling);  }})()
`
## show schema on the page
`
javascript:(function() {     var structuredData = document.querySelectorAll('script[type="application/ld+json"]');          if (structuredData.length === 0) {         alert("No structured data (JSON-LD) found on this page.");         return;     }          var jsonData = [];          structuredData.forEach(function(script) {         try {             var data = JSON.parse(script.textContent);             jsonData.push(data);         } catch (error) {             console.error("Error parsing JSON-LD:", error);         }     });          if (jsonData.length === 0) {         alert("No valid structured data (JSON-LD) found on this page.");         return;     }          var info = JSON.stringify(jsonData, null, 2);          var modal = document.createElement('div');     modal.style.position = 'fixed';     modal.style.top = '50%';     modal.style.left = '50%';     modal.style.transform = 'translate(-50%, -50%)';     modal.style.padding = '20px';     modal.style.background = 'white';     modal.style.border = '2px solid #ccc';     modal.style.zIndex = '9999';     modal.style.width = '80%';     modal.style.height = '80%';          var textArea = document.createElement("textarea");     textArea.value = info;     textArea.style.width = '100%';     textArea.style.height = '90%';     textArea.style.resize = 'none';     modal.appendChild(textArea);          var copyButton = document.createElement("button");     copyButton.textContent = "Copy";     copyButton.style.marginTop = '10px';     copyButton.style.padding = '5px 10px';     copyButton.style.background = '#007bff';     copyButton.style.color = '#fff';     copyButton.style.border = 'none';     copyButton.style.cursor = 'pointer';     copyButton.onclick = function() {         textArea.select();         document.execCommand("copy");         alert("Copied to clipboard!");     };     modal.appendChild(copyButton);          var closeButton = document.createElement("button");     closeButton.textContent = "Close";     closeButton.style.marginTop = '10px';     closeButton.style.padding = '5px 10px';     closeButton.style.background = '#007bff';     closeButton.style.color = '#fff';     closeButton.style.border = 'none';     closeButton.style.cursor = 'pointer';     closeButton.onclick = function() {         document.body.removeChild(modal);     };     modal.appendChild(closeButton);          document.body.appendChild(modal); })();
`
## show basic main meta data
`
javascript:(function() {    var title = document.title;    var description = document.querySelector('meta[name="description"]');    var canonical = document.querySelector('link[rel="canonical"]');    var noindex = document.querySelector('meta[name="robots"][content*="noindex"]');        var info = "Meta Title: " + title + "\n";        if(description)        info += "Meta Description: " + description.content + "\n";    else        info += "Meta Description: Not found\n";        if(canonical)        info += "Canonical URL: " + canonical.href + "\n";    else        info += "Canonical URL: Not found\n";        if(noindex)        info += "Noindex Tag: Found";    else        info += "Noindex Tag: Not found";        var modal = document.createElement('div');    modal.style.position = 'fixed';    modal.style.top = '50%';    modal.style.left = '50%';    modal.style.transform = 'translate(-50%, -50%)';    modal.style.padding = '20px';    modal.style.background = 'white';    modal.style.border = '2px solid #ccc';    modal.style.zIndex = '9999';    modal.style.width = '600px';    modal.style.height = '500px';        var textArea = document.createElement("textarea");    textArea.value = info;    textArea.style.width = '100%';    textArea.style.height = '70%';    textArea.style.resize = 'none';    modal.appendChild(textArea);        var copyButton = document.createElement("button");    copyButton.textContent = "Copy";    copyButton.style.marginTop = '10px';    copyButton.style.padding = '5px 10px';    copyButton.style.background = '#007bff';    copyButton.style.color = '#fff';    copyButton.style.border = 'none';    copyButton.style.cursor = 'pointer';    copyButton.onclick = function() {        textArea.select();        document.execCommand("copy");        alert("Copied to clipboard!");    };    modal.appendChild(copyButton);        var closeButton = document.createElement("button");    closeButton.textContent = "Close";    closeButton.style.marginTop = '10px';    closeButton.style.padding = '5px 10px';    closeButton.style.background = '#007bff';    closeButton.style.color = '#fff';    closeButton.style.border = 'none';    closeButton.style.cursor = 'pointer';    closeButton.onclick = function() {        document.body.removeChild(modal);    };    modal.appendChild(closeButton);        document.body.appendChild(modal);})();
`
## show all hreflang
`
javascript:(function() {    var hreflangs = document.querySelectorAll('link[rel="alternate"][hreflang]');        if (hreflangs.length === 0) {        alert("No hreflang tags found on this page.");        return;    }        var info = "Hreflang Languages and URLs:\n\n";        hreflangs.forEach(function(hreflang) {        var language = hreflang.getAttribute("hreflang");        var url = hreflang.getAttribute("href");                info += language + ": " + url + "\n";    });        var modal = document.createElement('div');    modal.style.position = 'fixed';    modal.style.top = '50%';    modal.style.left = '50%';    modal.style.transform = 'translate(-50%, -50%)';    modal.style.padding = '20px';    modal.style.background = 'white';    modal.style.border = '2px solid #ccc';    modal.style.zIndex = '9999';    modal.style.width = '500px';    modal.style.height = '400px';        var textArea = document.createElement("textarea");    textArea.value = info;    textArea.style.width = '100%';    textArea.style.height = '70%';    textArea.style.resize = 'none';    modal.appendChild(textArea);        var copyButton = document.createElement("button");    copyButton.textContent = "Copy";    copyButton.style.marginTop = '10px';    copyButton.style.padding = '5px 10px';    copyButton.style.background = '#007bff';    copyButton.style.color = '#fff';    copyButton.style.border = 'none';    copyButton.style.cursor = 'pointer';    copyButton.onclick = function() {        textArea.select();        document.execCommand("copy");        alert("Copied to clipboard!");    };    modal.appendChild(copyButton);        var closeButton = document.createElement("button");    closeButton.textContent = "Close";    closeButton.style.marginTop = '10px';    closeButton.style.padding = '5px 10px';    closeButton.style.background = '#007bff';    closeButton.style.color = '#fff';    closeButton.style.border = 'none';    closeButton.style.cursor = 'pointer';    closeButton.onclick = function() {        document.body.removeChild(modal);    };    modal.appendChild(closeButton);        document.body.appendChild(modal);})();
`

## open page in GSC
`
javascript:void(window.open(%27https://search.google.com%2Fsearch-console%2Fperformance%2Fsearch-analytics?resource_id=%27+window.location.protocol+%27%2F%2F%27+window.location.hostname+%27%2F&num_of_days=28&breakdown=query&page=!%27+window.location.href+%27&metrics=CLICKS%2CIMPRESSIONS%2CCTR%2CPOSITION&country=us%27,%27_blank%27));
`
## open page in semrush
`
javascript:(function() {    var currentUrl = encodeURIComponent(window.location.href);    var semrushUrl = 'https://www.semrush.com/analytics/overview/?q=%27%20+%20currentUrl;%20%20%20%20window.open(semrushUrl,%20%27_blank%27);})();
`
## Open page in page speed insights
`
javascript:(function() {
    var url = 'https://developers.google.com/speed/pagespeed/insights/?url=' + encodeURIComponent(window.location.href);
    window.open(url, '_blank');
})();
`
## Validate Schema
`
javascript:(function(){window.open('https://validator.schema.org/?url=' + encodeURIComponent(window.location.href));})();
`
