# Preface xtezza

This is "just" a fork from xtezza/mpdf-bundle. The puporse of this fork is to keep it installable with Symfony up to 7.x but I will NOT actively 
maintain it as long as it works for me. Also, I am no "pro" with composer and its versioning stuff. Nevertheless, feel free to use it at your own 
risk as long as you don't blame me for anything :)

If you choose to use it, adjust your `composer.json`
```
(...)
"repositories": [
	{
		"type": "vcs",
		"url": "https://github.com/xtezza/mpdf-bundle.git"
	}
],
(...)
"require" : {
	"xtezza/mpdf-bundle": "dev-master",
	(...)
}
(...)
```

# xtezza - Mpdf Bundle

Pdf generator for Symfony.

## What is it?

This is a Symfony Pdf Factory for use inside a controller to generate a PDF file from twig rendring using MPDF lib.

## Installation

### Step 1: Download HiddenEntityTypeBundle using composer
```bash
$ composer require xtezza/mpdf-bundle
```
Composer will install the bundle to your project's vendor directory.

### Step 2: Enable the bundle
Enable the bundle in the config if flex it did´nt do it for you:
```php
<?php
// config/bundles.php

return [
    // ...
    xtezza\MpdfBundle\SasedevMpdfBundle::class => ['all' => true],
    // ...
];
```

## Usage

You can use the factory in your controllers just like this:
```php
<?php

use xtezza\MpdfBundle\Factory\MpdfFactory;

// ...
public function pdf($id, Request $request, MpdfFactory $MpdfFactory) {
// ...
$mPdf = $MpdfFactory->createMpdfObject([
'mode' => 'utf-8',
'format' => 'A4',
'margin_header' => 5,
'margin_footer' => 5,
'orientation' => 'P'
]);
$mPdf->SetTopMargin("50");
$mPdf->SetHTMLHeader($this->renderView('twigfolder/pdf/pdf_header.html.twig', $TwigVars));
$mPdf->SetFooter($this->renderView('twigfolder/pdf/pdf_footer.html.twig', $TwigVars));
$mPdf->WriteHTML($this->renderView('twigfolder/pdf/pdf_content.html.twig', $TwigVars));
return $MpdfFactory->createDownloadResponse($mPdf, "file.pdf");
}
// ...
```
Or you can create a service

## Reporting an issue or a feature request
Feel free to report any issues. If you have an idea to make it better go ahead and modify and submit pull requests.

