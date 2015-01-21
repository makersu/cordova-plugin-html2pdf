## User Guide for Android by Maker Su
### add plugin
```
cordova plugin add https://github.com/makersu/makersu-cordova-plugin-html2pdf.git
```
### copy itextpdf-5.5.4.jar
```
cp plugins/at.modalog.cordova.plugin.html2pdf/itextpdf-5.5.4.jar platforms/android/libs/
```
### angularjs usage example
```
var saveFilename = 'xxx.pdf';
var savePath = device.platform == 'iOS' ? "~/Library/NoCloud/"+saveFilename : saveFilename;
var pdfPath = device.platform == 'iOS' ? cordova.file.dataDirectory+saveFilename : cordova.file.externalRootDirectory+saveFilename;
...
$scope.createAndDisplayPDF = function(filename) {
            $scope.showLoading();

            var success = function(status) {
                $scope.hideLoading();
                $state.go($state.$current, null, { reload: true });
                $scope.displayPDFFile(pdfPath); 
            };

            var error = function(status) {
                console.log(status);
            };

            $timeout(function() {
                var target=convert4PdfHtml()
                
                window.html2pdf.create(
                    angular.element(target).html(),
                    savePath,
                    success,
                    error
                );
            }, 200);

        }

```

Html 2 Pdf
=============

This is a pdf creation plugin for Phonegap 3.3.0 / Cordova 3.3.1 supporting Android (>=2.3.3) and iOS(>=6.0).
It creates a pdf from the given html and stores it on the device.

There is one method:

* create(html, filePath, successCallback, errorCallback)

Installation
======
You may use phonegap CLI as follows:

<pre>
➜ phonegap local plugin add https://github.com/moderna/cordova-plugin-html2pdf.git
[phonegap] adding the plugin: https://github.com/moderna/cordova-plugin-html2pdf.git
[phonegap] successfully added the plugin
</pre>

This Plugin requires iText.jar to be added to your project. Here is the last open source version (4.2.0) of it:    

 * GitHub: https://github.com/ymasory/iText-4.2.0
 * Download .jar:: https://github.com/ymasory/iText-4.2.0/downloads  
  
It has been confirmed to work with cordova 3.3.0+

Usage
====
```javascript
document.addEventListener('deviceready', onDeviceReady);
function onDeviceReady()
{
        var success = function(status) {
            alert('Message: ' + status);
        }

        var error = function(status) {
            alert('Error: ' + status);
        }

        window.html2pdf.create(
            "<html><head></head><body><h1>Some</h1><p>html content.</p></body></html>",
            "~/Documents/test.pdf", // on iOS,
			// "test.pdf", on Android (will be stored in /mnt/sdcard/at.modalog.cordova.plugin.html2pdf/test.pdf)
            success,
            error
        );
}
```


