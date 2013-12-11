WebMoney API PHP Library
========================

XML-interfaces supported
------------------------
- [X2](http://wiki.wmtransfer.com/projects/webmoney/wiki/Interface_X2): transferring funds from one purse to another
- [X3](https://wiki.wmtransfer.com/projects/webmoney/wiki/Interface_X3): receiving transaction history, checking transaction status
- [X8](http://wiki.wmtransfer.com/projects/webmoney/wiki/Interface_X8): retrieving information about purse ownership, searching for system user by his/her identifier or purse
- [X9](https://wiki.wmtransfer.com/projects/webmoney/wiki/Interface_X9): retrieving information about purse balance
- [X11](http://wiki.wmtransfer.com/projects/webmoney/wiki/Interface_X11): retrieving information from client’s passport by WM-identifier
- [X17](http://wiki.wmtransfer.com/projects/webmoney/wiki/Interface_X17): operations with arbitration contracts
- [X18](http://wiki.wmtransfer.com/projects/webmoney/wiki/Interface_X18): getting transaction details via merchant.webmoney
- [X19](http://wiki.wmtransfer.com/projects/webmoney/wiki/Interface_X19): verifying personal information for the owner of a WM identifier

Capitaller interfaces supported
-------------------------------
- [SendWM](http://www.capitaller.ru/ws/DoPayment.asmx?op=SendWM): funds transfer
- [SendWMOA](http://www.capitaller.ru/ws/DoPayment.asmx?op=SendWMOA): funds transfer, сonsidering recipient authorization
- [SendWMProt](http://www.capitaller.ru/ws/DoPayment.asmx?op=SendWMProt): funds transfer with protection

Megastock interfaces supported
------------------------------
- Interface for [adding Payment Integrator's merchants](http://www.megastock.ru/Doc/AddIntMerchant.aspx?lang=en)
- Interface for [check status of merchant Payment Integrator](http://www.megastock.ru/Doc/AddIntMerchant.aspx)

Requirements
------------
The library requires PHP 5.3 compiled with [cURL extension](http://www.php.net/manual/en/book.curl.php) (but you can override cURL dependencies).

To use signing with the WM Kepper Classic keys you have to compile PHP with [BCMath](http://www.php.net/manual/en/book.bc.php) and [GMP](http://www.php.net/manual/en/book.gmp.php) support.

To use Capitaller API you have to compile PHP with [SOAP](http://www.php.net/manual/en/book.soap.php) support.

Example
-------
```php
require_once(__DIR__ . '/vendor/autoload.php'); // Require autoload file generated by composer

use Baibaratsky\WebMoney;

$webMoney = new WebMoney\WebMoney(new WebMoney\Request\RequestPerformer\CurlRequestPerformer);

$x9request = new WebMoney\Api\X\X9\Request;
$x9request->setSignerWmid('your WMID');
$x9request->setRequestedWmid('requested WMID');
$x9request->sign(new WebMoney\Request\RequestSigner('wmid', 'key', 'password'));

if ($x9request->validate()) {
    $x9response = $webMoney->request($x9request);
}
```
