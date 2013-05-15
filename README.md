KitpagesPDFBundle
=================

Pdf: FPDF and FPDI simple wrapper for Symfony


Installation
============
use composer update

add the new Bundle in app/appKernel.php

Use example
============

use Kitpages\PDFBundle\lib\PDF;


$pdf = new PDF();
$pagecount = $pdf->setSourceFile('oldPdf.pdf);

for($i = 1; $i <= $pagecount; $i++){
    $tplIdx = $pdf->importPage($i);
    $s = $pdf->getTemplatesize($tplIdx);
    $pdf->AddPage($s['h'] > $s['w'] ? 'P' : 'L', array($s['w'], $s['h']), true); // This gets it the right dimensions
    $pdf->useTemplate($tplIdx, 0, 0, 0, 0, true);
    $pdf->SetFont('Arial','',8);
    $pdf->SetTextColor(168,168,168);
    $pdf->SetY(20);
    $pdf->SetX(80);
    $pdf->Write(0, 'modify my pdf');
}
$pdf->Output('newPdf.pdf, 'D');
