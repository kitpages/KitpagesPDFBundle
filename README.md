KitpagesPDFBundle
=================

Pdf: FPDF and FPDI simple wrapper for Symfony

Installation
============

Step 1: Download the Bundle
---------------------------

Open a command console, enter your project directory and execute the
following command to download the latest stable version of this bundle:

```bash
$ composer require "kitpages/pdf-bundle": "dev-master as 1.0"
```

This command requires you to have Composer installed globally, as explained
in the [installation chapter](https://getcomposer.org/doc/00-intro.md)
of the Composer documentation.

Step 2: Enable the Bundle
-------------------------

Then, enable the bundle by adding the following line in the `app/AppKernel.php`
file of your project:

```php
<?php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = array(
            // ...

            new Kitpages\PDFBundle\KitpagesPDFBundle(),
        );

        // ...
    }

    // ...
}
```

Step 3: Use the Bundle
----------------------

```php
        // ...
    public function indexAction()
    {
        // ...
        $pdf = new PDF();

        $pagecount = $pdf->setSourceFile('oldPdf.pdf');

        for($i = 1; $i <= $pagecount; $i++) {

            $tplIdx = $pdf->importPage($i);

            $s = $pdf->getTemplatesize($tplIdx);

            // This gets it the right dimensions
            $pdf->AddPage($s['h'] > $s['w'] ? 'P' : 'L', array($s['w'], $s['h']), true); 
            $pdf->useTemplate($tplIdx, 0, 0, 0, 0, true);

            $pdf->SetFont('Arial','',8);
            $pdf->SetTextColor(168,168,168);

            $pdf->SetY(20);
            $pdf->SetX(80);

            $pdf->Write(0, 'modify my pdf');
        }

        $pdf->Output('newPdf.pdf', 'D');
        
        return $this->render('default/index.html.twig');
    }
```
