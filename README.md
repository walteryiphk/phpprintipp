Manually copy the 5 php files (*IPP.php +  http_class.php) in a same directory. It can be a 'printipp' directory in your project, preferably out of the web-accessable path, or, better, a directory in your php include_path (eg c:\php\includes", see your php.ini file) for a system-wide installation.
Manually copy — if needed the unpacked archive's bin/*.php in a system's directory PATH included.
Manually copy the unpacked archive's /documentation where you want — preferably in a local web repository directory, in order file links works.
you'll have to put either one of the following lines in your PHP code, depending of what level of operations you want to perform (only one include/require is needed, because top-classes will load automagically the low-level ones):

      require_once('printipp/BasicIPP.php');
    or:
      require_once('printipp/PrintIPP.php');
    or:
      require_once('printipp/ExtendedPrintIPP.php');
    or:
      require_once('printipp/CupsPrintIPP.php');
    
Choose the last if you are unsure
