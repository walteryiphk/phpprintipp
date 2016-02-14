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


<h1>PHP PrintIPP usage</h1>

  <div class='menu'>
    <h2>Summary</h2>

    <dl>
      <dt><span class="h2"><a href="#introduction">Introduction</a></span></dt>

      <dt><span class="h2"><a href="#basicusage">Basic usage</a></span></dt>

      <dt><span class="h2"><a href="#advancedusage">Advanced
      usage</a></span></dt>

      <dt><span class="h2"><a href="#known-problems">Why do it doesn't work?
      Huh!</a></span></dt>

      <dt><span class="h2"><a href="#variables">Public
      variables</a></span></dt>

      <dd>
        <dl>
          <dt><span class="h3"><a href="#setupvar">setup public
          variables</a></span></dt>

          <dd>
            <dl class="final">
              <dt><a href='#s1'>$ssl</a></dt>

              <dt><a href='#s2'>$paths</a></dt>

              <dt><a href='#s3'>$http_timeout</a></dt>

              <dt><a href='#s4'>$http_data_timeout</a></dt>

              <dt><a href='#s5'>$debug_level</a></dt>

              <dt><a href='#s6'>$alert_on_end_tag</a></dt>

              <dt><a href='#s7'>$with_exceptions</a></dt>

              <dt><a href='#s8'>$handle_http_exceptions</a></dt>
            </dl>
          </dd>

          <dt><span class="h3"><a href="#readvar">readable public
          variables</a></span></dt>

          <dd>
            <dl class="final">
              <dt><a href='#a1'>$jobs</a></dt>

              <dt><a href='#a2'>$jobs_uri</a></dt>

              <dt><a href='#a3'>$status</a></dt>

              <dt><a href='#a4'>$response_completed</a></dt>

              <dt><a href='#a5'>$last_job</a></dt>

              <dt><a href='#a6'>$printer_attributes</a></dt>

              <dt><a href='#a7'>$job_attributes</a></dt>

              <dt><a href='#a8'>$jobs_attributes</a></dt>

              <dt><a href='#a9'>$available_printers</a></dt>

              <dt><a href='#a10'>$printers_uri</a></dt>

              <dt><a href='#a11'>$debug</a></dt>

              <dt><a href='#a12'>$attributes</a></dt>
            </dl>
          </dd>
        </dl>
      </dd>

      <dt><span class="h2"><a href="#responseparsing">Response
      parsing</a></span></dt>

      <dt><span class="h2"><a href="#functionsreference">Functions
      reference</a></span></dt>

      <dd>
        <dl>
          <dt><span class="h3"><a href="#funcsetup">Setup</a></span></dt>

          <dd>
            <dl class="final">
              <dt><a href='#b1'>setPort($port='631')</a></dt>

              <dt><a href='#b2'>setHost($host='localhost')</a></dt>

              <dt><a href=
              '#b25'>setUnix($socket='/var/run/cups/cups.sock')</a></dt>

              <dt><a href='#b3'>setPrinterUri($uri)</a></dt>

              <dt><a href='#b4'>setData($data)</a></dt>

              <dt><a href='#b5'>setRawText()</a></dt>

              <dt><a href='#b6'>unsetRawText()</a></dt>

              <dt><a href='#b7'>setBinary()</a></dt>

              <dt><a href='#b8'>setFormFeed()</a></dt>

              <dt><a href='#b9'>unsetFormFeed()</a></dt>

              <dt><a href='#b10'>setCharset($charset)</a></dt>

              <dt><a href='#b11'>setLanguage($language)</a></dt>

              <dt><a href=
              '#b12'>setMimeMediaType($mime_media_type='application/octet-stream')</a></dt>

              <dt><a href='#b13'>setCopies($nbrcopies=1)</a></dt>

              <dt><a href='#b14'>setDocumentName($document_name)</a></dt>

              <dt><a href=
              '#b15'>setJobName($jobname='(PHP)',$absolute=false)</a></dt>

              <dt><a href='#b16'>setUserName($username='PHP-SERVER')</a></dt>

              <dt><a href=
              '#b17'>setAuthentication($username,$password)</a></dt>

              <dt><a href='#b18'>setSides($sides=2)</a></dt>

              <dt><a href='#b19'>setFidelity()</a></dt>

              <dt><a href='#b20'>unsetFidelity()</a></dt>

              <dt><a href='#b21'>setMessage($message)</a></dt>

              <dt><a href='#b22'>setPageRanges($page_ranges)</a></dt>

              <dt><a href='#b23'>setAttribute($attribute,$value)</a></dt>

              <dt><a href='#b24'>unsetAttribute($attribute)</a></dt>
            </dl>
          </dd>

          <dt><span class="h3"><a href="#funcops">Operations</a></span></dt>

          <dd>
            <dl class="final">
              <dt><a href='#c1'>printJob()</a></dt>

              <dt><a href='#c2'>cancelJob($job_uri)</a></dt>

              <dt><a href='#c3'>getPrinterAttributes()</a></dt>

              <dt><a href='#c4'>validateJob()</a></dt>

              <dt><a href=
              '#c5'>getJobAttributes($job_uri,subset="false",$attributes_group="all")</a></dt>

              <dt><a href=
              '#c6'>getJobs($my_jobs=true,$limit=0,$which_jobs="",$subset='true')</a></dt>

              <dt><a href='#c7'>printURI($uri)</a></dt>

              <dt><a href='#c8'>purgeJobs()</a></dt>

              <dt><a href='#c9'>createJob()</a></dt>

              <dt><a href='#c10'>sendDocument($job_uri,$is_last=false)</a></dt>

              <dt><a href='#c11'>sendURI($uri,$job_uri,$is_last=false)</a></dt>

              <dt><a href='#c12'>pausePrinter()</a></dt>

              <dt><a href='#c13'>resumePrinter()</a></dt>

              <dt><a href='#c14'>holdJob($job_uri,$until='indefinite')</a></dt>

              <dt><a href='#c15'>releaseJob($job_uri)</a></dt>

              <dt><a href='#c16'>restartJob($job_uri)</a></dt>

              <dt><a href=
              '#c17'>setJobAttributes($job_uri,array($deleted_attributes))</a></dt>

              <dt><a href='#c18'>getPrinters()</a></dt>
            </dl>
          </dd>

          <dt><span class="h3"><a href="#funclog">Logging /
          Debugging</a></span></dt>

          <dd>
            <dl class="final">
              <dt><a href=
              '#d1'>setLog($log_destination,$destination_type='file',$level=2)</a></dt>

              <dt><a href='#d2'>printDebug()</a></dt>

              <dt><a href='#d3'>getDebug()</a></dt>
            </dl>
          </dd>
        </dl>
      </dd>

      <dt><span class="h2"><a href="#exceptions">Exceptions</a></span></dt>

      <dd>
        <dl class="final">
          <dt><a href="#e1">httpException</a></dt>
        </dl>

        <dl class="final">
          <dt><a href="#e2">ippException</a></dt>
        </dl>
      </dd>

      <dt><span class="h2"><a href="#attributes">writable
      attributes</a></span></dt>

      <dt><span class="h2"><a href="#readable-attributes">readable
      attributes</a></span></dt>

      <dt><span class="h2"><a href="#CupsPrintIPP-usage">Cups specific
      operations and parsing</a></span></dt>

      <dt><span class="h2"><a href="#phpprintipp">phpprintipp command line
      tool</a></span></dt>

      <dt><span class="h2">Distribution</span></dt>

      <dd>
        <dl>
          <dt><a href="#copyright">Copyright of this document</a></dt>

          <dt><a href="#codelicense">Copyright of non trivial code
          examples</a></dt>

          <dt><a href="#license">GNU Free Documentation License</a></dt>

          <dt><a href="#license2">GNU General Public License</a></dt>
        </dl>
      </dd>
    </dl>
  </div>

  <div class="section" id="introduction">
    <h2>Introduction</h2>

    <p>PHP PrintIPP is a PHP5 class library. It is designed to easier usage of
    Internet Printing Protocol.</p>

    <p>It makes easy simple actions like print and cancel a document, and not
    difficult complex tasks as print a text document on 2 pages per sheet, dual
    sided, with staples on center (provided your printer and print server
    does).</p>
  </div>

  <div class="section" id="basicusage">
    <h2>Basic usage</h2>

    <p>As we said, simple things are simple:</p>
    <pre class="pre">
                &lt;?php
                
                    require_once(PrintIPP.php);
                    
                    $ipp = new PrintIPP();
                    
                    $ipp-&gt;setHost("localhost");
                    $ipp-&gt;setPrinterURI("/printers/epson");
                    $ipp-&gt;setData("./testfiles/test-utf8.txt"); // Path to file.
                    $ipp-&gt;printJob();

                ?&gt;
            
</pre>

    <p class="note">You can replace filename by a string.</p>
    <pre class="pre">
                 &lt;?php
                    
                    $ipp-&gt;setAuthentication("test","test"); // system username &amp; password, need to be lpadmin
                    
                    $job = $ipp-&gt;last_job; // getting job uri
                    
                    $ipp-&gt;cancelJob($job); // cancelling job

                 ?&gt;
            
</pre>
  </div>

  <div class="section" id="advancedusage">
    <h2>A little more</h2>

    <p>Now, we making little more complex tasks:</p>
    <pre class="pre">

                &lt;?php
                /* printing an utf-8 file, two-sided, two pages per sheet */   

                    
                    require_once(PrintIPP.php);

                    $ipp = new PrintIPP();
                    $ipp-&gt;setHost("localhost");
                    $ipp-&gt;setPrinterURI("/printers/epson");
                    
                    $ipp-&gt;debug_level = 3; // Debugging very verbose
                    $ipp-&gt;setLog('/tmp/printipp','file',3); // logging very verbose
                    $ipp-&gt;setUserName("foo bar"); // setting user name for server
                    $ipp-&gt;setDocumentName("testfile with UTF-8 characters");
                    $ipp-&gt;setCharset('utf-8');

                    
                    $ipp-&gt;setAttribute('number-up',2);
                    $ipp-&gt;setSides(); //     by default:  2 = two-sided-long-edge
                                        //  other choices:  1 = one-sided
                                        //                  2CE = two-sided-short-edge
                    
                    $ipp-&gt;setData("./testfiles/test-utf8.txt");//Path to file.
                    printf(_("Job status: %s"), $ipp-&gt;printJob()); // Print job, display job status

                    $ipp-&gt;printDebug(); // display debugging output
                
                ?&gt;
                
            
</pre>
    <pre class="pre">

                &lt;?php
                /* printing selected pages from document */   

                    
                    $ipp-&gt;setDocumentName("Selected parts of GNU FDL");
                    
                    $ipp-&gt;setAttribute('number-up',4); // 4 pages per sheet
                    $ipp-&gt;setAttribute('media','A7'); // very little pages
                    $ipp-&gt;setPageRanges('1:2 5:6'); // print only pages 1 to 2 and 5 to 6
                    
                    $ipp-&gt;setData("./documentation/COPYING");//Path to file.
                    
                    $ipp-&gt;printJob();
                
                    $ipp-&gt;setPageRanges(''); // reset page ranges
                    
                ?&gt;
                 
            
</pre>
    <pre class="pre">
                &lt;?php
                
                /* printing strings, no form feed */

                    $ipp-&gt;setRawText();
                    $ipp-&gt;unsetFormFeed();

                    $ipp-&gt;setData("This is a line\n");
                    $ipp-&gt;printJob();

                    $ipp-&gt;setData("This is half a line ");
                    $ipp-&gt;printJob();

                    $ipp-&gt;setData("This is a end of line\n");
                    $ipp-&gt;printJob("epson");

                    // set copies to 2 (same sheet of paper: form feed is unset)
                    $ipp-&gt;setData("This lines must appeared twice\r\n");
                    $ipp-&gt;setCopies(2);
                    $ipp-&gt;printJob();
                    
                    $ipp-&gt;setCopies(1);

                    // printing string, then form feed
                    $ipp-&gt;setFormFeed();
                    $ipp-&gt;setData("End of test");
                    $ipp-&gt;printJob();

                    $ipp-&gt;setBinary(); // reset to normal use
                    
                    echo "Jobs URIs:"; // display jobs uris
                    echo "&lt;pre&gt;\n";
                    print_r($ipp-&lt;jobs_uri);
                    echo "&lt;/pre&gt;";


                ?&gt;
            
</pre>

    <p class="note">Raw text is not usable for laser printers.</p>
  </div>

  <div class="section" id="known-problems">
    <h2>Problems and solutions</h2>

    <div class="subsection">
      <h3>My script fails with "_(): function unknown"</h3>

      <div class="subsubsection">
        <div>
          OK: you do not have gettext (gettext is an I-18n
          (internationalization) system).
        </div>

        <div>
          Solutions:

          <dl>
            <dt>Install gettext part of PHP</dt>

            <dd>The simpler one if you have your own server</dd>

            <dt>Create a fake gettext</dt>

            <dd>
              in your code:
              <pre>
                                        if (!function_exists('_'))
                                           require_once ('gettext.php');
                                    
</pre>File gettext.php:
              <pre>
                                        &lt;?php
                                            function _($text) {
                                                return $text;
                                            }
                                        &gt;
                                    
</pre>That's all!
            </dd>
          </dl>
        </div>
      </div>
    </div>
  </div>

  <div class="section" id="variables">
    <h2>Public variables</h2>

    <div class="subsection" id="setupvar">
      <h3>Setup</h3>

      <div class="subsubsection">
        <h4><a id='s1' name="s1">$ssl</a></h4>Set it to 1 for tls connections
        between web server and IPP server.

        <p class="note">With CUPS1.1, you need to setup "SSLPort" in
        "cupsd.conf" on wanted port for secure connections</p>
      </div>

      <div class="subsubsection">
        <h4><a id='s2' name="s2">$paths</a></h4>array<br>
        keys = root,admin,printers,jobs<br>
        Set paths to whatever needed for the operations. By default, CUPS
        server settings (values = "/","/admin/","/printers/","/jobs/").
      </div>

      <div class="subsubsection">
        <h4><a id='s3' name="s3">$http_timeout</a></h4>timeout at http
        connection (seconds) 0 &rArr; default &rArr; 30.
      </div>

      <div class="subsubsection">
        <h4><a id='s4' name="s4">$http_data_timeout</a></h4>data reading
        timeout (milliseconds) 0 &rArr; default &rArr; 30.
      </div>

      <div class="subsubsection">
        <h4><a id='s5' name="s5">$debug_level</a></h4>0 to 4 (4 = quiet).
        Debugging purpose, set the amount of data you want for
        get/printDebug().
      </div>

      <div class="subsubsection">
        <h4><a id='s6' name="s6">$alert_on_end_tag</a></h4>debugging purpose:
        echo "END tag OK" if (1 and reads while end tag). If you experience
        problems with incomplete responses from server, you can use it to setup
        $http_data_timeout.
      </div>

      <div class="subsubsection">
        <h4><a id='s7' name="s7">$with_exceptions</a></h4>Set it to true to
        activate exceptions (backward compatibility).
      </div>

      <div class="subsubsection">
        <h4><a id='s8' name="s8">$handle_http_exceptions</a></h4>Set it to true
        to activate handling of http exceptions through ippException.
      </div>
    </div>

    <div class="subsection" id="readvar">
      <h3>Readable public variables</h3>

      <div class="subsubsection">
        <h4><a id='a1' name="a1">$jobs</a></h4>array()<br>
        contains job ids from operations (filled with non null value if such a
        job is returned by server, eg. after "PrintJob()").
      </div>

      <div class="subsubsection">
        <h4><a id='a2' name="a2">$jobs_uri</a></h4>array()<br>
        contains job URIs from operations. What you must read if you want to
        cancel job or make other operations on it.
      </div>

      <div class="subsubsection">
        <h4><a id='a3' name="a3">$status</a></h4>array()<br>
        exit status from each operation.
      </div>

      <div class="subsubsection">
        <h4><a id='a4' name="a4">$response_completed</a></h4>array()<br>
        If you suspect incomplete responses from server, contains information
        about it ("no" or "complete" for each operation).
      </div>

      <div class="subsubsection">
        <h4><a id='a5' name="a5">$last_job</a></h4>string<br>
        contains last job's URI. Useful for CancelJob().
      </div>

      <div class="subsubsection">
        <h4><a id='a6' name="a6">$printer_attributes</a></h4>object you can
        read: printer's attributes after getPrinterAttributes().
      </div>

      <div class="subsubsection">
        <h4><a id='a7' name="a7">$job_attributes</a></h4>object you can read:
        last job attributes.
      </div>

      <div class="subsubsection">
        <h4><a id='a8' name="a8">$jobs_attributes</a></h4>object you can read:
        jobs attributes after getJobs().
      </div>

      <div class="subsubsection">
        <h4><a id='a9' name="a9">$available_printers</a></h4>array<br>
        printers URIS after getPrinters() if such getPrinters operation is
        implemented for your vendor (Currently: CUPS).
      </div>

      <div class="subsubsection">
        <h4><a id='a10' name="a10">$printers_uri</a></h4>array<br>
        printers URIs for each job, if returned by server (not with CUPS).
      </div>

      <div class="subsubsection">
        <h4><a id='a11' name="a11">$debug</a></h4>array<br>
        debugging information, 1 line per event logged.
      </div>

      <div class="subsubsection">
        <h4><a id='a12' name="a12">$attributes</a></h4>object you can read:
        attributes after any operation.
      </div>
    </div>
  </div>

  <div class="section" id="responseparsing">
    <h2>Response parsing</h2>

    <div class="subsection">
      <h3>Operation's status</h3>Returned by operations functions.<br>
      Can also be found in array $ipp-&gt;status (1 key by operation).

      <p class="note">Operations functions returns false in case of HTTP
      error,</p>
    </div>

    <div class="subsection">
      <h3>Job's uri</h3>Needed to CancelJob($job_uri).<br>
      Last job uri is in string $ipp-&gt;last_job<br>
      Can also be found in array $ipp-&gt;jobs_uri (1 key by operation);
    </div>

    <div class="subsection">
      <h3>Available printer's uris</h3>Found in array
      $ipp-&gt;available_printers, after a call to getPrinters().

      <p class="note">getPrinters() is not part of IPP standard, thus it is
      implemented in (NameOfVendor)PrintIPP.</p>
    </div>

    <div class="subsection">
      <h3>Printer's attributes</h3>After a call to getPrinterAttributes(),
      founds in $ipp-&gt;printer_attributes.<br>
      example:
      <pre class="pre">
                &lt;?php

                    $ipp = new PrintIPP();
                    $ipp-&gt;setHost("localhost");
                    $ipp-&gt;setPort();
                    $ipp-&gt;setPrinterURI("/printers/epson");
                    
                    $ipp-&gt;getPrinterAttributes();
                    
                    echo "Printer attributes for printer $i:
                    &lt;pre&gt;\n"; print_r($ipp-&gt;printer_attributes); echo "&lt;/pre&gt;";
                    
                    /* Cups defines an attribute "printer -type" */
                        if (isset($ipp-&gt;printer_attributes-&gt;printer_type-&gt;_value2)
                        &amp;&amp; ($ipp-&gt;printer_attributes-&gt;printer_type-&gt;_value2) == 'print-black')
                        echo "The printer can print black&lt;br /&gt;\n";
                        
                        if (isset($ipp-&gt;printer_attributes-&gt;printer_type-&gt;_value3)
                        &amp;&amp; ($ipp-&gt;printer_attributes-&gt;printer_type-&gt;_value3) == 'print-color')
                        echo "The printer can print color&lt;br /&gt;\n";
                    
                    /* other attributes */
                        echo "Printer State: ".$ipp-&gt;printer_attributes-&gt;printer_state-&gt;_value0."&lt;br /&gt;\n";
                        echo "Printer State message: ".$ipp-&gt;printer_attributes-&gt;printer_state_message-&gt;_value0."&lt;br /&gt;";
                        
                        echo "Document formats supported:&lt;br /&gt;&lt;pre&gt;";
                        $pointer = "_value0";
                        for ($i = 0 ; isset($ipp-&gt;printer_attributes-&gt;document_format_supported-&gt;$pointer); $i++) {
                            echo $ipp-&gt;printer_attributes-&gt;document_format_supported-&gt;$pointer . "\n";
                            $pointer = "_value" . ($i + 1);
                            }
                        echo "&lt;/pre&gt;";

 
                ?&gt;
                    
</pre>
    </div>

    <div class="subsection">
      <h3>Job's attributes</h3>After a call to *Job() (except "validateJob"),
      founds in $ipp-&gt;job_attributes.<br>
      Parsing: same method than Printer's attributes. see <a href=
      "#getJobAttributes">getJobAttributes() operation</a>;
    </div>

    <div class="subsection">
      <h3>Job's attributes</h3>After a call to getJobs(), founds in
      $ipp-&gt;jobs_attributes.<br>
      Parsing: same method than Printer's attributes, except that jobs
      <em>are</em> objects. See "getJobs()" operation for an example.
    </div>
  </div>

  <div class="section" id="functionsreference">
    <h2>Functions reference</h2>

    <div class="subsection" id="funcsetup">
      <h3>Setup</h3>

      <div class="subsubsection">
        <h4><a id='b1' name="b1">setPort($port='631')</a></h4>Select port which
        IPP server listen. By default port is set to IANA assigned port (631).
      </div>

      <div class="subsubsection">
        <h4><a id='b2' name="b2">setHost($host='localhost')</a></h4>Select host
        which is located IPP server (IP or resolvable hostname/FQDN).
        <span class='important'>(! &acirc;&dagger;&rsquo; disable setUnix()
        ).</span> <span class='important'>Mandatory if you dont use UNIX
        sockets.</span>
      </div>

      <div class="subsubsection">
        <h4><a id='b25' name=
        "b25">setUnix($socket='/var/run/cups/cups.sock')</a></h4>Set UNIX
        socket name <span class='important'>(! &acirc;&dagger;&rsquo; disable
        setHost()).</span> <span class='important'>Mandatory if you don't use
        http/https.</span>
      </div>

      <div class="subsubsection">
        <h4><a id='b3' name="b3">setPrinterUri($uri)</a></h4>Select printer.
        <pre class="pre">
                    /* examples */
                    
                    $ipp-&gt;setPrinterUri('/printers/epson');
                    $ipp-&gt;setPrinterUri('ipp://localhost:631/printers/epson')
                    
</pre><span class='important'>Mandatory, automatically done by <a href=
"CupsPrintIPP-usage.html">CupsPrintIPP</a> if not set.</span>
      </div>

      <div class="subsubsection">
        <h4><a id='b4' name="b4">setData($data)</a></h4>string to be printed or
        file name of a <em>readable</em> file. <span class=
        'important'>Mandatory for printing operations PrintJob() &amp;
        sendDocument().</span>
      </div>

      <div class="subsubsection">
        <h4><a id='b5' name="b5">setRawText()</a></h4>Force data to be
        interpreted as raw text, and be sent directly to printer. It prepends a
        "SYN" and postpend a "Form Feed" characters to the data or file.

        <p class='note'>Can be used only on dot-matrix and ink-jet
        printers.</p>
      </div>

      <div class="subsubsection">
        <h4><a id='b6' name="b6">unsetRawText()</a></h4>Unset previous
        operation (setRawText()).
      </div>

      <div class="subsubsection">
        <h4><a id='b7' name="b7">setBinary()</a></h4>Alias for unsetRawText().
      </div>

      <div class="subsubsection">
        <h4><a id='b8' name="b8">setFormFeed()</a></h4>When rawText is set,
        forces a form feed after printing. Automatically set at setRawText()
        call.
      </div>

      <div class="subsubsection">
        <h4><a id='b9' name="b9">unsetFormFeed()</a></h4>Causes not form feed
        in RawText mode.

        <p class='note'>Must be called <em>after</em> each occurrence of
        setRawText.</p>
      </div>

      <div class="subsubsection">
        <h4><a id='b10' name="b10">setCharset($charset)</a></h4>Set requests
        charset. Automatically set to "us-ascii" if not set.
      </div>

      <div class="subsubsection">
        <h4><a id='b11' name="b11">setLanguage($language)</a></h4>Set requests
        natural language. Automatically set to "en_us" if not set.
      </div>

      <div class="subsubsection">
        <h4><a id='b12' name=
        "b12">setMimeMediaType($mime_media_type='application/octet-stream')</a></h4>Set
        type of document. By default: application/octet-stream &rArr; auto
        detection.
      </div>

      <div class="subsubsection">
        <h4><a id='b13' name="b13">setCopies($nbrcopies=1)</a></h4>Set number
        of copies.
      </div>

      <div class="subsubsection">
        <h4><a id='b14' name="b14">setDocumentName($document_name)</a></h4>Set
        document name (as for title page).
      </div>

      <div class="subsubsection">
        <h4><a id='b15' name=
        "b15">setJobName($jobname='(PHP)',$absolute=false)</a></h4>Set job
        name. If $absolute is not 'true' (default), a count is automatically
        appended (MMDDHHMMSScount).
      </div>

      <div class="subsubsection">
        <h4><a id='b16' name=
        "b16">setUserName($username='PHP-SERVER')</a></h4>Set user name as
        displayed on server and title pages. Automatically set to "PHP-SERVER"
        if not.
      </div>

      <div class="subsubsection">
        <h4><a id='b17' name=
        "b17">setAuthentication($username,$password)</a></h4>Set system user
        name and password when server needs authentication for operation. (e.g.
        cancelJob() on CUPS with standard settings).

        <p class="note">If the server do not support Basic nor Digest
        authentication, you need to install SASL to use authentication. See
        INSTALL</p>
      </div>

      <div class="subsubsection">
        <h4><a id='b18' name="b18">setSides($sides=2)</a></h4>Set sides on
        printed document.<br>
        Possibles values are:

        <dl>
          <dt>1: one-sided</dt>

          <dt>2: two-sided-long-edge</dt>

          <dt>2CE: two-sided-short-edge</dt>
        </dl>
      </div>

      <div class="subsubsection">
        <h4><a id='b19' name="b19">setFidelity()</a></h4>If printer can't
        respect all attributes, do not print.
      </div>

      <div class="subsubsection">
        <h4><a id='b20' name="b20">unsetFidelity()</a></h4>Print anyway
        (replace attributes as needed), after a call to setFidelity ().
      </div>

      <div class="subsubsection">
        <h4><a id='b21' name="b21">setMessage($message)</a></h4>Set message
        given to user, especially with CancelJob().

        <p class='note'>Cups does not reply this message</p>
      </div>

      <div class="subsubsection">
        <h4><a id='b22' name="b22">setPageRanges($page_ranges)</a></h4>Set
        ranges of pages to be printed. $page_ranges&nbsp;==&nbsp;string,
        e.g.:"&nbsp;1-2&nbsp;5-6&nbsp;8-14".<br>

        <p class="note">an empty string resets page-ranges.</p>
      </div>

      <div class="subsubsection">
        <h4><a id='b23' name="b23">setAttribute($attribute,$value)</a></h4>For
        attributes which have not dedicated function. $attribute and $value are
        the correspondent text strings in RFC2911. Returns false on
        failure.<br>
        Examples:
        <pre class='pre'>
                    
                    /* standard */
                    
                    $ipp-&gt;setAttribute("job-billing", "Thomas");
                    
                    /* with 1 set of xxx */
                   
                     // add a start banner "confidential" and a end banner "secret"
                     // I know, this example is unusual
                    $ipp-&gt;setAttribute("job-sheets", array("confidential","secret"));
                    
                    /* special case for resolution: */
                    
                        // dpi: dot per inch
                    $ipp-&gt;setAttribute("printer-resolution","1440x720dpi");
                    
                        // dpc: dot per centimeter
                    $ipp-&gt;setAttribute("printer-resolution","320x200dpc");
                    
                    
</pre>setAttributes takes care of attribute-type: you have to enter the text
string, comprised 'enum' types.<br>
        Will add a separate page to list attributes and parameters, but for
        starting you cant get most of them by "getPrinterAttributes()" and
        "getJobAttributes()" :)
      </div>

      <div class="subsubsection">
        <h4><a id='b24' name="b24">unsetAttribute($attribute)</a></h4>Unset
        given attribute for next jobs, for attributes which have not dedicated
        function.
      </div>
    </div>

    <div class="subsection" id="funcops">
      <h3>Operations</h3>

      <div class="subsubsection">
        <h4><a id='c1' name="c1">printJob()</a></h4>Print a single string or
        document, previously set by setdata($data).
      </div>

      <div class="subsubsection">
        <h4><a id='c2' name="c2">cancelJob($job_uri)</a></h4>cancel job which
        have uri $uri, as which is given in $ipp-&gt;last_job or in array
        $ipp-&gt;jobs_uri&nbsp;&rArr;&nbsp;(one key by operation).
      </div>

      <div class="subsubsection">
        <h4><a id='c3' name="c3">getPrinterAttributes()</a></h4>Get printer's
        attributes of printer set by setPrinterUri($uri), fill object
        $ipp-&gt;printer_attributes. see <a href="#responseparsing">response
        parsing</a>.
      </div>

      <div class="subsubsection">
        <h4><a id='c4' name="c4">validateJob()</a></h4>Verify if the job can be
        printed with it's attributes before sending document.<br>
        Example:
        <pre class="pre">
                    
                    &lt;?php
                    
                    [...]
                    $ipp-&gt;setMimeMediaType("application/x-foobar");
                    
                    echo "Validate-Job: ".$ipp-&gt;validateJob()."&lt;br /&gt;";

                    foreach ($ipp-&gt;attributes as $name =&gt; $attribute)
                        if ($attribute-&gt;_range == 'unsupported-attributes')
                            printf('%s "%s": unsupported attribute&lt;br /&gt;',$name,$attribute-&gt;_value0);
                        
                    reset($ipp-&gt;attributes);
                    
                    ?&gt;
                    
                    <span class="normal">Displays:</span>
                    Validate-Job: client-error-document-format-not-supported
                    document_format "application/x-foobar": unsupported attribute
                    
                    
</pre>
      </div>

      <div class="subsubsection" id="getJobAttributes">
        <h4><a id='c5' name=
        "c5">getJobAttributes($job_uri,subset="false",$attributes_group="all")</a></h4>Get
        attributes from the job $job_uri. If (!$subset), gives
        $attributes_group="all" by default, or attributes_group =
        'job-template' or 'job-description' if you fills third argument. if
        ($subset), gives only useful subset of attributes.<br>
        Example:
        <pre class="pre">
                    &lt;?php
                    
                    [...]
                    echo "Printing Job: ".$ipp-&gt;printJob()."&lt;br /&gt;";
                    $ipp-&gt;getJobAttributes($ipp-&gt;last_job,false,'job-template');
                    
                    $job_state = $ipp-&gt;job_attributes-&gt;job_state-&gt;_value0;
                    echo "Job-State: $job_state&lt;br /&gt;";

                    $job_state_reasons = $ipp-&gt;job_attributes-&gt;job_state_reasons-&gt;_value0;
                    echo "Job-State-Reasons: $job_state_reasons&lt;br /&gt;";
                    
                    echo "&lt;pre&gt;";print_r($ipp-&gt;job_attributes); echo "&lt;/pre&gt;";
                    
                    ?&gt;
                    
                    <span class="normal">displays:</span>
                    Job-State: processing
                    Job-State-Reasons: job-printing
                        <span class=
"normal">(or whatever is the job's status)</span>
                   stdClass Object
                   (
                       [attributes_charset] =&gt; stdClass Object
                               (
                                [_type] =&gt; charset
                                [_range] =&gt; start operation-attributes
                                [_value0] =&gt; utf-8
                                )

                       [attributes_natural_language] =&gt; stdClass Object
                               (
                                [_type] =&gt; naturalLanguage
                                [_range] =&gt; start operation-attributes
                                [_value0] =&gt; fr-fr
                               )
 
                       [job_uri] =&gt; stdClass Object
                               (
                                [_type] =&gt; uri
                                [_range] =&gt; start job-attributes
                                [_value0] =&gt; http://geekette:631/jobs/202
                                )
                       [...]
                    
</pre>
      </div>

      <div class="subsubsection">
        <h4><a id='c6' name=
        "c6">getJobs($my_jobs=true,$limit=0,$which_jobs="",$subset='true')</a></h4>get
        Jobs attributes, by default only your jobs, except if you set first
        argument to "false", by default with no limit, except if you gives an
        integer (0 &lt; x &lt; 65535) in second argument, by default
        not-completed, except if you gives 'completed' as third argument, by
        default only a useful subset of attributes, except if you gives 'false'
        as fourth argument.<br>
        Example:
        <pre class="pre">
                    &lt;?php
                    
                    echo "Getting Jobs: ".$ipp-&gt;getJobs($my_jobs=true,$limit=0,"completed",true)."&lt;br /&gt;";
                    echo "Job 0 state: ".$ipp-&gt;jobs_attributes-&gt;job_0-&gt;job_state-&gt;_value0."&lt;br /&gt;";
                    echo "Job 0 state-reasons: ".$ipp-&gt;jobs_attributes-&gt;job_0-&gt;job_state_reasons-&gt;_value0."&lt;br /&gt;";
                    
                    echo "&lt;pre&gt;";print_r($ipp-&gt;jobs_attributes); echo "&lt;/pre&gt;";
                    
                    ?&gt;

                    <span class='normal'>Displays:</span>
                    Getting Jobs: successful-ok-ignored-or-substituted-attributes
                    Job 0 state: processing
                    Job 0 state-reasons: job-printing
                    
                    stdClass Object
                                    (
                                     [job_0] =&gt; stdClass Object
                                            (
                                             [job_more_info] =&gt; stdClass Object
                                                (
                                                 [_type] =&gt; uri
                                                 [_range] =&gt; start job-attributes
                                                 [_value0] =&gt; http://geekette:631/jobs/205
                                                 )
                                             [job_uri] =&gt; stdClass Object
                                                (
                                                 [_type] =&gt; uri
                                                 [_range] =&gt; start job-attributes
                                                 [_value0] =&gt; http://geekette:631/jobs/205
                                                )
                                             [job_printer_up_time] =&gt; stdClass Object
                                                (
                                                 [_type] =&gt; integer
                                                 [_range] =&gt; start job-attributes
                                                 [_value0] =&gt; 1136224652
                                                )
                                             [job_name] =&gt; stdClass Object
                                               (
                                                [_type] =&gt; nameWithoutLanguage
                                                [_range] =&gt; start job-attributes
                                                [_value0] =&gt; test-utf8.txt
                                               )
                                             [job_state] =&gt; stdClass Object
                                               (
                                                [_type] =&gt; enum
                                                [_range] =&gt; start job-attributes
                                                [_value0] =&gt; processing
                                               )
                                             [job_state_reasons] =&gt; stdClass Object
                                               (
                                                [_type] =&gt; keyword
                                                [_range] =&gt; start job-attributes
                                                [_value0] =&gt; job-printing
                                               )
                                            )
                                     [job_1] =&gt; stdClass Object
                                        [...]
                                    )
                    
</pre>
      </div>

      <div class="subsubsection">
        <h4><a id='c7' name="c7">printURI($uri)</a></h4>

        <p class="note">Implemented in ExtendedPrintIPP.</p>Print a single
        document, which uri is given in argument.

        <p class="note">Not implemented in Cups server (OPTIONAL
        operation).</p>
      </div>

      <div class="subsubsection">
        <h4><a id='c8' name="c8">purgeJobs()</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP</p>Purge jobs
        for printer designed by setPrinterUri($uri), for all printers if $uri
        is "/printers/".<br>
        Example:
        <pre class="pre">
                    
                    &lt;?php
                    
                    /* purging jobs for a printer */

                    $IPP = new ExtendedPrintIPP();
                    
                    $ipp-&gt;setUserName("test");
                    $ipp-&gt;setAuthentication("test","test"); // username &amp; password 
                    $ipp-&gt;setPrinterURI("ipp://localhost:631/printers/epson"); // Set printer URI here
                    echo "Purge-Jobs: ". $ipp-&gt;purgeJobs() ."&lt;br /&gt;";

                    /* purging jobs for all printers */
                    $ipp-&gt;setPrinterURI("ipp://localhost:631/printers/"); // =&gt; all printers
                    echo "Purge-Jobs: ". $ipp-&gt;purgeJobs() ."&lt;br /&gt;";

                    ?&gt;
                    
</pre>
      </div>

      <div class="subsubsection">
        <h4><a id='c9' name="c9">createJob()</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>IPP
        Create-Job operation, before sending multi-documents with
        sendDocument($job); or sendURI($job,$uri).<br>
        See sendDocument example.
      </div>

      <div class="subsubsection">
        <h4><a id='c10' name=
        "c10">sendDocument($job_uri,$is_last=false)</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>Send a
        document after a job has been created.<br>
        Example:
        <pre class="pre">
                    &lt;?php
                    
                    function __autoload($class_name) {
                        require_once $class_name . '.php';
                        }
 
                    $IPP = new ExtendedPrintIPP();
                    
                    $ipp-&gt;debug_level = 3;
                    $ipp-&gt;setUserName("test");
                    $ipp-&gt;setCopies(2);
                    
                    $ipp-&gt;setAuthentication("test","test"); // username &amp; password. MANDATORY
                    
                    echo "Create-Job: ".$ipp-&gt;createJob(). "&lt;br /&gt;";
                    printf("Job is: %s&lt;br /&gt;",$job = $ipp-&gt;last_job);
                    echo "&lt;pre&gt;";print_r($ipp-&gt;job_attributes);echo "&lt;/pre&gt;\n";

                    $ipp-&gt;setDocumentName("test-utf8.txt");
                    $ipp-&gt;setData("./testfiles/test-utf8.txt");
                    echo "Sending document: " . $ipp-&gt;sendDocument($job) . "&lt;br /&gt;\n";

                    $ipp-&gt;setDocumentName("text string");
                    $ipp-&gt;setData("This is the string of second document");
                    echo "Sending document: " . $ipp-&gt;sendDocument($job,$last=true) . "&lt;br /&gt;\n";

                    // must be refused. Hem: CUPS is very smart, it accepts :)
                    echo "Sending document: " . $ipp-&gt;sendDocument($job,$last=true) . "&lt;br /&gt;\n";

                    ?&gt;
                    
</pre>
      </div>

      <div class="subsubsection">
        <h4><a id='c11' name=
        "c11">sendURI($uri,$job_uri,$is_last=false)</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>Send a
        document after a job has been created.<br>
        Example:
        <pre class="pre">
                    &lt;?php
                    
                    $uri = "http://localhost/";
                    
                    echo "Create-Job: ".$ipp-&gt;createJob(). "&lt;br /&gt;";
                    printf("Job is: %s&lt;br /&gt;",$job = $ipp-&gt;last_job);
 
                    echo "Sending URI: " . $ipp-&gt;sendURI($uri,$job,$last=true) . "&lt;br /&gt;\n";

                    ?&gt;
                    
</pre>
      </div>

      <div class="subsubsection">
        <h4><a id='c12' name="c12">pausePrinter()</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>Pause
        printer setted by setPrinterURI($uri).
      </div>

      <div class="subsubsection">
        <h4><a id='c13' name="c13">resumePrinter()</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>resume
        (restart) printer set by setPrinterURI($uri).
      </div>

      <div class="subsubsection">
        <h4><a id='c14' name=
        "c14">holdJob($job_uri,$until='indefinite')</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>Holds a
        job.<br>
        $until can
        be'no-hold','day-time','evening','night','weekend','second-shift','third-shift'.<br>

        Example:
        <pre class="pre">
                    &lt;?php
                    
                    echo "printing document: " . $ipp-&gt;printJob("test"). "&lt;br /&gt;\n";

                    echo "Holding Job: " .$ipp-&gt;holdJob($job,'night');
                    
                    $ipp-&gt;getJobAttributes($ipp-&gt;last_job,false,'job-template');
                    
                    $job_state = $ipp-&gt;job_attributes-&gt;job_state-&gt;_value0;
                    echo "Job-State: $job_state&lt;br /&gt;";

                    $job_state_reasons = $ipp-&gt;job_attributes-&gt;job_state_reasons-&gt;_value0;
                    echo "Job-State-Reasons: $job_state_reasons&lt;br /&gt;";
                     
                    ?&gt;
                    
</pre>
      </div>

      <div class="subsubsection">
        <h4><a id='c15' name="c15">releaseJob($job_uri)</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>Release a
        pending or holded job.
      </div>

      <div class="subsubsection">
        <h4><a id='c16' name="c16">restartJob($job_uri)</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>Restarts a
        completed job.<br>
        Example:
        <pre class="pre">
                    &lt;?php
                    
                    echo "printing document: " . $ipp-&gt;printJob("test"). "&lt;br /&gt;\n";
                    
                    sleep (10);
                    
                    $ipp-&gt;setAttribute('job-hold-until','weekend');
                    
                    $ipp-&gt;restartJob($ipp-&gt;last_job);
                    
                     
                    ?&gt;
                    
                    Will re-print the job in the week-end.
                    
</pre>
      </div>

      <div class="subsubsection">
        <h4><a id='c17' name=
        "c17">setJobAttributes($job_uri,array($deleted_attributes))</a></h4>

        <p class="note">Function implemented in ExtendedPrintIPP.</p>Modify
        <em>an existing job's</em> attributes with values previously set by
        various setXXX operations.<br>
        Delete attributes which are in array of second argument.<br>
        Example:
        <pre class="pre">
                        
                        /* setting copies to 2 */
                    
                    $ipp-&gt;setCopies(2);
                    
                        /* no idea for what to delete :) */

                    $unset_attributes = array();

                        /* commit changes */

                    $ipp-&gt;setJobAttributes($ipp-&gt;last_job,$unset_attributes); 
                    
                    
</pre>
      </div>

      <div class="subsubsection">
        <h4><a id='c18' name="c18">getPrinters()</a></h4>

        <p class="note">Function implemented in (NameOfVendor)PrintIPP.</p>Get
        availables printers, fill array $ipp-&gt;available_printers with
        printer's uris.<br>
        Example:
        <pre class="pre">
                    
                    &lt;?php
                       
                        function __autoload($class_name) {
                            require_once $class_name . '.php';
                        }
                        
                        $ipp = new CupsPrintIPP;
                        
                        $ipp-&gt;getPrinters();
                        
                        $uri = $ipp-&gt;available_printers[0];
                        
                        $ipp-&gt;setPrinterUri($uri);
                        
                    ?&gt;
                    
                    
</pre>
      </div>
    </div>

    <div class="subsection" id="funclog">
      <h3>Logging / debugging</h3>

      <div class="subsubsection">
        <h4><a id='d1' name=
        "d1">setLog($log_destination,$destination_type='file',$level=2)</a></h4>$destination_type
        can be "file", "logger", "e-mail".<br>
        $log_destination is a (new) writable file in a writable directory, or
        e-mail.<br>
        $level is

        <dl>
          <dt>0 &rArr; quiet;</dt>

          <dt>1 to 3 &rArr; less to more verbose.</dt>
        </dl>
      </div>

      <div class="subsubsection">
        <h4><a id='d2' name="d2">printDebug()</a></h4>Display debugging
        information.<br>
        Verbosity set from 0 to 4 (=silent) in $ipp-&gt;debug_level.
      </div>

      <div class="subsubsection">
        <h4><a id='d3' name="d3">getDebug()</a></h4>Returns debugging
        information.<br>
        Verbosity set from 0 to 4 (=silent) in $ipp-&gt;debug_level.
      </div>
    </div>
  </div>

  <div class="section" id="exceptions">
    <h2>Exceptions</h2>

    <div class="subsection" id="e1">
      <h3>httpException</h3>

      <dl>
        <dt>public function getErrorFormatted()</dt>

        <dt>public function getErrno()</dt>

        <dt>public function getMessage()</dt>

        <dt>public function getLine()</dt>

        <dt>public function getFile()</dt>

        <dt>public function getTrace()</dt>

        <dt>public function getTraceAsString()</dt>
      </dl>
    </div>

    <div class="subsection" id="e2">
      <h3>ippException</h3>

      <dl>
        <dt>public function getErrorFormatted()</dt>

        <dt>public function getErrno()</dt>

        <dt>public function getMessage()</dt>

        <dt>public function getLine()</dt>

        <dt>public function getFile()</dt>

        <dt>public function getTrace()</dt>

        <dt>public function getTraceAsString()</dt>
      </dl>
    </div>
  </div>

  <div class="section" id="attributes">
    <h2>writable attributes</h2>

    <p>See file <a href="attributes.html">attributes.html</a></p>
  </div>

  <div class="section" id="readable-attributes">
    <h2>Readable attributes</h2>

    <p>See file <a href=
    "readable-attributes.html">readable-attributes.html</a></p>
  </div>

  <div class="section" id="CupsPrintIPP-usage">
    <h2>Cups specific operations and parsing</h2>

    <p>See file <a href=
    "CupsPrintIPP-usage.html">CupsPrintIPP-usage.html</a></p>
  </div>

  <div class="section" id="phpprintipp">
    <h2>phpprintipp command line tool</h2>

    <p>See file <a href="phpprintipp.html">phpprintipp.html</a></p>
  </div>

  <div class="section" id="copyright">
    <h2>Copyright / Distribution of this document</h2>

    <div class="subsection">
      <h3>Copyright of this document</h3>

      <p>Copyright &Acirc;&copy; 2005-2008 Thomas Harding.</p>

      <p>Due to non-<a href=
      'http://www.debian.org/social_contract#guidelines'>DFSG</a> compliance of
      GFDL, this document is distributed under dual licence :</p>

      <ol>
        <li>The GNU Free Documentation License</li>

        <li>The GNU General Public License</li>
      </ol>

      <p class='typewriter'>Permission is granted to copy, distribute and/or
      modify this document under the terms of the GNU Free Documentation
      License, Version 1.2 or any later version published by the Free Software
      Foundation; with no Invariant Sections, no Front-Cover Texts, and no
      Back-Cover Texts. A copy of the license is included in the section
      entitled "GNU Free Documentation License".</p>

      <p class='typewriter'>These files are free software; you can redistribute
      them and/or modify them under the terms of the GNU General Public License
      as published by the Free Software Foundation; either version 2 of the
      License, or (at your option) any later version. This documentation is
      distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY;
      without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
      PARTICULAR PURPOSE. See the GNU General Public License for more details.
      You should have received a copy of the GNU General Public License along
      with this documentation; if not, write to the Free Software Foundation,
      Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA</p>
    </div>

    <div class="subsection">
      <h3 id='codelicense'>Copyright of non trivial code examples</h3>

      <p>Copyright &Acirc;&copy; 2005-2006 Thomas Harding.</p>
      <pre class="pre">
                    All rights reserved.
  
                    Redistribution and use in source and binary forms, with or without
                    modification, are permitted provided that the following conditions are
                    met:
 
                    Redistribution of source code must retain the above copyright
                    notice, this list of conditions and the following disclaimer.
                    Redistribution's in binary form must reproduce the above copyright
                    notice, this list of conditions and the following disclaimer in the
                    documentation and/or other materials provided with the distribution.
                    Neither the name of its Author nor the names of its
                    contributors may be used to endorse or promote products derived from
                    this software without specific prior written permission.

                    THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
                    IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
                    THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
                    PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR
                    CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
                    EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
                    PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
                    PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
                    LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
                    NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
                    SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
                  
</pre>
    </div>

    <div class="subsection">
      <h3 id="license">GNU Free Documentation License</h3>
      <pre class="pre">
                GNU Free Documentation License
                  Version 1.2, November 2002


 Copyright (C) 2000,2001,2002  Free Software Foundation, Inc.
     51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.


0. PREAMBLE

The purpose of this License is to make a manual, textbook, or other
functional and useful document "free" in the sense of freedom: to
assure everyone the effective freedom to copy and redistribute it,
with or without modifying it, either commercially or non-commercially.
Secondarily, this License preserves for the author and publisher a way
to get credit for their work, while not being considered responsible
for modifications made by others.

This License is a kind of "copyleft", which means that derivative
works of the document must themselves be free in the same sense.  It
complements the GNU General Public License, which is a copyleft
license designed for free software.

We have designed this License in order to use it for manuals for free
software, because free software needs free documentation: a free
program should come with manuals providing the same freedoms that the
software does.  But this License is not limited to software manuals;
it can be used for any textual work, regardless of subject matter or
whether it is published as a printed book.  We recommend this License
principally for works whose purpose is instruction or reference.


1. APPLICABILITY AND DEFINITIONS

This License applies to any manual or other work, in any medium, that
contains a notice placed by the copyright holder saying it can be
distributed under the terms of this License.  Such a notice grants a
world-wide, royalty-free license, unlimited in duration, to use that
work under the conditions stated herein.  The "Document", below,
refers to any such manual or work.  Any member of the public is a
licensee, and is addressed as "you".  You accept the license if you
copy, modify or distribute the work in a way requiring permission
under copyright law.

A "Modified Version" of the Document means any work containing the
Document or a portion of it, either copied verbatim, or with
modifications and/or translated into another language.

A "Secondary Section" is a named appendix or a front-matter section of
the Document that deals exclusively with the relationship of the
publishers or authors of the Document to the Document's overall subject
(or to related matters) and contains nothing that could fall directly
within that overall subject.  (Thus, if the Document is in part a
textbook of mathematics, a Secondary Section may not explain any
mathematics.)  The relationship could be a matter of historical
connection with the subject or with related matters, or of legal,
commercial, philosophical, ethical or political position regarding
them.

The "Invariant Sections" are certain Secondary Sections whose titles
are designated, as being those of Invariant Sections, in the notice
that says that the Document is released under this License.  If a
section does not fit the above definition of Secondary then it is not
allowed to be designated as Invariant.  The Document may contain zero
Invariant Sections.  If the Document does not identify any Invariant
Sections then there are none.

The "Cover Texts" are certain short passages of text that are listed,
as Front-Cover Texts or Back-Cover Texts, in the notice that says that
the Document is released under this License.  A Front-Cover Text may
be at most 5 words, and a Back-Cover Text may be at most 25 words.

A "Transparent" copy of the Document means a machine-readable copy,
represented in a format whose specification is available to the
general public, that is suitable for revising the document
straightforwardly with generic text editors or (for images composed of
pixels) generic paint programs or (for drawings) some widely available
drawing editor, and that is suitable for input to text formatters or
for automatic translation to a variety of formats suitable for input
to text formatters.  A copy made in an otherwise Transparent file
format whose markup, or absence of markup, has been arranged to thwart
or discourage subsequent modification by readers is not Transparent.
An image format is not Transparent if used for any substantial amount
of text.  A copy that is not "Transparent" is called "Opaque".

Examples of suitable formats for Transparent copies include plain
ASCII without markup, Texinfo input format, LaTeX input format, SGML
or XML using a publicly available DTD, and standard-conforming simple
HTML, PostScript or PDF designed for human modification.  Examples of
transparent image formats include PNG, XCF and JPG.  Opaque formats
include proprietary formats that can be read and edited only by
proprietary word processors, SGML or XML for which the DTD and/or
processing tools are not generally available, and the
machine-generated HTML, PostScript or PDF produced by some word
processors for output purposes only.

The "Title Page" means, for a printed book, the title page itself,
plus such following pages as are needed to hold, legibly, the material
this License requires to appear in the title page.  For works in
formats which do not have any title page as such, "Title Page" means
the text near the most prominent appearance of the work's title,
preceding the beginning of the body of the text.

A section "Entitled XYZ" means a named subunit of the Document whose
title either is precisely XYZ or contains XYZ in parentheses following
text that translates XYZ in another language.  (Here XYZ stands for a
specific section name mentioned below, such as "Acknowledgements",
"Dedications", "Endorsements", or "History".)  To "Preserve the Title"
of such a section when you modify the Document means that it remains a
section "Entitled XYZ" according to this definition.

The Document may include Warranty Disclaimers next to the notice which
states that this License applies to the Document.  These Warranty
Disclaimers are considered to be included by reference in this
License, but only as regards disclaiming warranties: any other
implication that these Warranty Disclaimers may have is void and has
no effect on the meaning of this License.


2. VERBATIM COPYING

You may copy and distribute the Document in any medium, either
commercially or noncommercially, provided that this License, the
copyright notices, and the license notice saying this License applies
to the Document are reproduced in all copies, and that you add no other
conditions whatsoever to those of this License.  You may not use
technical measures to obstruct or control the reading or further
copying of the copies you make or distribute.  However, you may accept
compensation in exchange for copies.  If you distribute a large enough
number of copies you must also follow the conditions in section 3.

You may also lend copies, under the same conditions stated above, and
you may publicly display copies.


3. COPYING IN QUANTITY

If you publish printed copies (or copies in media that commonly have
printed covers) of the Document, numbering more than 100, and the
Document's license notice requires Cover Texts, you must enclose the
copies in covers that carry, clearly and legibly, all these Cover
Texts: Front-Cover Texts on the front cover, and Back-Cover Texts on
the back cover.  Both covers must also clearly and legibly identify
you as the publisher of these copies.  The front cover must present
the full title with all words of the title equally prominent and
visible.  You may add other material on the covers in addition.
Copying with changes limited to the covers, as long as they preserve
the title of the Document and satisfy these conditions, can be treated
as verbatim copying in other respects.

If the required texts for either cover are too voluminous to fit
legibly, you should put the first ones listed (as many as fit
reasonably) on the actual cover, and continue the rest onto adjacent
pages.

If you publish or distribute Opaque copies of the Document numbering
more than 100, you must either include a machine-readable Transparent
copy along with each Opaque copy, or state in or with each Opaque copy
a computer-network location from which the general network-using
public has access to download using public-standard network protocols
a complete Transparent copy of the Document, free of added material.
If you use the latter option, you must take reasonably prudent steps,
when you begin distribution of Opaque copies in quantity, to ensure
that this Transparent copy will remain thus accessible at the stated
location until at least one year after the last time you distribute an
Opaque copy (directly or through your agents or retailers) of that
edition to the public.

It is requested, but not required, that you contact the authors of the
Document well before redistributing any large number of copies, to give
them a chance to provide you with an updated version of the Document.


4. MODIFICATIONS

You may copy and distribute a Modified Version of the Document under
the conditions of sections 2 and 3 above, provided that you release
the Modified Version under precisely this License, with the Modified
Version filling the role of the Document, thus licensing distribution
and modification of the Modified Version to whoever possesses a copy
of it.  In addition, you must do these things in the Modified Version:

A. Use in the Title Page (and on the covers, if any) a title distinct
   from that of the Document, and from those of previous versions
   (which should, if there were any, be listed in the History section
   of the Document).  You may use the same title as a previous version
   if the original publisher of that version gives permission.
B. List on the Title Page, as authors, one or more persons or entities
   responsible for authorship of the modifications in the Modified
   Version, together with at least five of the principal authors of the
   Document (all of its principal authors, if it has fewer than five),
   unless they release you from this requirement.
C. State on the Title page the name of the publisher of the
   Modified Version, as the publisher.
D. Preserve all the copyright notices of the Document.
E. Add an appropriate copyright notice for your modifications
   adjacent to the other copyright notices.
F. Include, immediately after the copyright notices, a license notice
   giving the public permission to use the Modified Version under the
   terms of this License, in the form shown in the Addendum below.
G. Preserve in that license notice the full lists of Invariant Sections
   and required Cover Texts given in the Document's license notice.
H. Include an unaltered copy of this License.
I. Preserve the section Entitled "History", Preserve its Title, and add
   to it an item stating at least the title, year, new authors, and
   publisher of the Modified Version as given on the Title Page.  If
   there is no section Entitled "History" in the Document, create one
   stating the title, year, authors, and publisher of the Document as
   given on its Title Page, then add an item describing the Modified
   Version as stated in the previous sentence.
J. Preserve the network location, if any, given in the Document for
   public access to a Transparent copy of the Document, and likewise
   the network locations given in the Document for previous versions
   it was based on.  These may be placed in the "History" section.
   You may omit a network location for a work that was published at
   least four years before the Document itself, or if the original
   publisher of the version it refers to gives permission.
K. For any section Entitled "Acknowledgements" or "Dedications",
   Preserve the Title of the section, and preserve in the section all
   the substance and tone of each of the contributor acknowledgements
   and/or dedications given therein.
L. Preserve all the Invariant Sections of the Document,
   unaltered in their text and in their titles.  Section numbers
   or the equivalent are not considered part of the section titles.
M. Delete any section Entitled "Endorsements".  Such a section
   may not be included in the Modified Version.
N. Do not retitle any existing section to be Entitled "Endorsements"
   or to conflict in title with any Invariant Section.
O. Preserve any Warranty Disclaimers.

If the Modified Version includes new front-matter sections or
appendices that qualify as Secondary Sections and contain no material
copied from the Document, you may at your option designate some or all
of these sections as invariant.  To do this, add their titles to the
list of Invariant Sections in the Modified Version's license notice.
These titles must be distinct from any other section titles.

You may add a section Entitled "Endorsements", provided it contains
nothing but endorsements of your Modified Version by various
parties--for example, statements of peer review or that the text has
been approved by an organization as the authoritative definition of a
standard.

You may add a passage of up to five words as a Front-Cover Text, and a
passage of up to 25 words as a Back-Cover Text, to the end of the list
of Cover Texts in the Modified Version.  Only one passage of
Front-Cover Text and one of Back-Cover Text may be added by (or
through arrangements made by) any one entity.  If the Document already
includes a cover text for the same cover, previously added by you or
by arrangement made by the same entity you are acting on behalf of,
you may not add another; but you may replace the old one, on explicit
permission from the previous publisher that added the old one.

The author(s) and publisher(s) of the Document do not by this License
give permission to use their names for publicity for or to assert or
imply endorsement of any Modified Version.


5. COMBINING DOCUMENTS

You may combine the Document with other documents released under this
License, under the terms defined in section 4 above for modified
versions, provided that you include in the combination all of the
Invariant Sections of all of the original documents, unmodified, and
list them all as Invariant Sections of your combined work in its
license notice, and that you preserve all their Warranty Disclaimers.

The combined work need only contain one copy of this License, and
multiple identical Invariant Sections may be replaced with a single
copy.  If there are multiple Invariant Sections with the same name but
different contents, make the title of each such section unique by
adding at the end of it, in parentheses, the name of the original
author or publisher of that section if known, or else a unique number.
Make the same adjustment to the section titles in the list of
Invariant Sections in the license notice of the combined work.

In the combination, you must combine any sections Entitled "History"
in the various original documents, forming one section Entitled
"History"; likewise combine any sections Entitled "Acknowledgements",
and any sections Entitled "Dedications".  You must delete all sections
Entitled "Endorsements".


6. COLLECTIONS OF DOCUMENTS

You may make a collection consisting of the Document and other documents
released under this License, and replace the individual copies of this
License in the various documents with a single copy that is included in
the collection, provided that you follow the rules of this License for
verbatim copying of each of the documents in all other respects.

You may extract a single document from such a collection, and distribute
it individually under this License, provided you insert a copy of this
License into the extracted document, and follow this License in all
other respects regarding verbatim copying of that document.


7. AGGREGATION WITH INDEPENDENT WORKS

A compilation of the Document or its derivatives with other separate
and independent documents or works, in or on a volume of a storage or
distribution medium, is called an "aggregate" if the copyright
resulting from the compilation is not used to limit the legal rights
of the compilation's users beyond what the individual works permit.
When the Document is included in an aggregate, this License does not
apply to the other works in the aggregate which are not themselves
derivative works of the Document.

If the Cover Text requirement of section 3 is applicable to these
copies of the Document, then if the Document is less than one half of
the entire aggregate, the Document's Cover Texts may be placed on
covers that bracket the Document within the aggregate, or the
electronic equivalent of covers if the Document is in electronic form.
Otherwise they must appear on printed covers that bracket the whole
aggregate.


8. TRANSLATION

Translation is considered a kind of modification, so you may
distribute translations of the Document under the terms of section 4.
Replacing Invariant Sections with translations requires special
permission from their copyright holders, but you may include
translations of some or all Invariant Sections in addition to the
original versions of these Invariant Sections.  You may include a
translation of this License, and all the license notices in the
Document, and any Warranty Disclaimers, provided that you also include
the original English version of this License and the original versions
of those notices and disclaimers.  In case of a disagreement between
the translation and the original version of this License or a notice
or disclaimer, the original version will prevail.

If a section in the Document is Entitled "Acknowledgements",
"Dedications", or "History", the requirement (section 4) to Preserve
its Title (section 1) will typically require changing the actual
title.


9. TERMINATION

You may not copy, modify, sublicense, or distribute the Document except
as expressly provided for under this License.  Any other attempt to
copy, modify, sublicense or distribute the Document is void, and will
automatically terminate your rights under this License.  However,
parties who have received copies, or rights, from you under this
License will not have their licenses terminated so long as such
parties remain in full compliance.


10. FUTURE REVISIONS OF THIS LICENSE

The Free Software Foundation may publish new, revised versions
of the GNU Free Documentation License from time to time.  Such new
versions will be similar in spirit to the present version, but may
differ in detail to address new problems or concerns.  See
http://www.gnu.org/copyleft/.

Each version of the License is given a distinguishing version number.
If the Document specifies that a particular numbered version of this
License "or any later version" applies to it, you have the option of
following the terms and conditions either of that specified version or
of any later version that has been published (not as a draft) by the
Free Software Foundation.  If the Document does not specify a version
number of this License, you may choose any version ever published (not
as a draft) by the Free Software Foundation.


ADDENDUM: How to use this License for your documents

To use this License in a document you have written, include a copy of
the License in the document and put the following copyright and
license notices just after the title page:

    Copyright (c)  YEAR  YOUR NAME.
    Permission is granted to copy, distribute and/or modify this document
    under the terms of the GNU Free Documentation License, Version 1.2
    or any later version published by the Free Software Foundation;
    with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.
    A copy of the license is included in the section entitled "GNU
    Free Documentation License".

If you have Invariant Sections, Front-Cover Texts and Back-Cover Texts,
replace the "with...Texts." line with this:

    with the Invariant Sections being LIST THEIR TITLES, with the
    Front-Cover Texts being LIST, and with the Back-Cover Texts being LIST.

If you have Invariant Sections without Cover Texts, or some other
combination of the three, merge those two alternatives to suit the
situation.

If your document contains nontrivial examples of program code, we
recommend releasing these examples in parallel under your choice of
free software license, such as the GNU General Public License,
to permit their use in free software.
            
</pre>
    </div>

    <div class="subsection">
      <h3 id="license2">GNU General Public License</h3>
      <pre class="pre">
                    GNU GENERAL PUBLIC LICENSE
                       Version 2, June 1991

 Copyright (C) 1989, 1991 Free Software Foundation, Inc.
                       51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.

                            Preamble

  The licenses for most software are designed to take away your
freedom to share and change it.  By contrast, the GNU General Public
License is intended to guarantee your freedom to share and change free
software--to make sure the software is free for all its users.  This
General Public License applies to most of the Free Software
Foundation's software and to any other program whose authors commit to
using it.  (Some other Free Software Foundation software is covered by
the GNU Library General Public License instead.)  You can apply it to
your programs, too.

  When we speak of free software, we are referring to freedom, not
price.  Our General Public Licenses are designed to make sure that you
have the freedom to distribute copies of free software (and charge for
this service if you wish), that you receive source code or can get it
if you want it, that you can change the software or use pieces of it
in new free programs; and that you know you can do these things.

  To protect your rights, we need to make restrictions that forbid
anyone to deny you these rights or to ask you to surrender the rights.
These restrictions translate to certain responsibilities for you if you
distribute copies of the software, or if you modify it.

  For example, if you distribute copies of such a program, whether
gratis or for a fee, you must give the recipients all the rights that
you have.  You must make sure that they, too, receive or can get the
source code.  And you must show them these terms so they know their
rights.

  We protect your rights with two steps: (1) copyright the software, and
(2) offer you this license which gives you legal permission to copy,
distribute and/or modify the software.

  Also, for each author's protection and ours, we want to make certain
that everyone understands that there is no warranty for this free
software.  If the software is modified by someone else and passed on, we
want its recipients to know that what they have is not the original, so
that any problems introduced by others will not reflect on the original
authors' reputations.

  Finally, any free program is threatened constantly by software
patents.  We wish to avoid the danger that redistributors of a free
program will individually obtain patent licenses, in effect making the
program proprietary.  To prevent this, we have made it clear that any
patent must be licensed for everyone's free use or not licensed at all.

  The precise terms and conditions for copying, distribution and
modification follow.

                    GNU GENERAL PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. This License applies to any program or other work which contains
a notice placed by the copyright holder saying it may be distributed
under the terms of this General Public License.  The "Program", below,
refers to any such program or work, and a "work based on the Program"
means either the Program or any derivative work under copyright law:
that is to say, a work containing the Program or a portion of it,
either verbatim or with modifications and/or translated into another
language.  (Hereinafter, translation is included without limitation in
the term "modification".)  Each licensee is addressed as "you".

Activities other than copying, distribution and modification are not
covered by this License; they are outside its scope.  The act of
running the Program is not restricted, and the output from the Program
is covered only if its contents constitute a work based on the
Program (independent of having been made by running the Program).
Whether that is true depends on what the Program does.

  1. You may copy and distribute verbatim copies of the Program's
source code as you receive it, in any medium, provided that you
conspicuously and appropriately publish on each copy an appropriate
copyright notice and disclaimer of warranty; keep intact all the
notices that refer to this License and to the absence of any warranty;
and give any other recipients of the Program a copy of this License
along with the Program.

You may charge a fee for the physical act of transferring a copy, and
you may at your option offer warranty protection in exchange for a fee.

  2. You may modify your copy or copies of the Program or any portion
of it, thus forming a work based on the Program, and copy and
distribute such modifications or work under the terms of Section 1
above, provided that you also meet all of these conditions:

    a) You must cause the modified files to carry prominent notices
    stating that you changed the files and the date of any change.

    b) You must cause any work that you distribute or publish, that in
    whole or in part contains or is derived from the Program or any
    part thereof, to be licensed as a whole at no charge to all third
    parties under the terms of this License.

    c) If the modified program normally reads commands interactively
    when run, you must cause it, when started running for such
    interactive use in the most ordinary way, to print or display an
    announcement including an appropriate copyright notice and a
    notice that there is no warranty (or else, saying that you provide
    a warranty) and that users may redistribute the program under
    these conditions, and telling the user how to view a copy of this
    License.  (Exception: if the Program itself is interactive but
    does not normally print such an announcement, your work based on
    the Program is not required to print an announcement.)

These requirements apply to the modified work as a whole.  If
identifiable sections of that work are not derived from the Program,
and can be reasonably considered independent and separate works in
themselves, then this License, and its terms, do not apply to those
sections when you distribute them as separate works.  But when you
distribute the same sections as part of a whole which is a work based
on the Program, the distribution of the whole must be on the terms of
this License, whose permissions for other licensees extend to the
entire whole, and thus to each and every part regardless of who wrote it.

Thus, it is not the intent of this section to claim rights or contest
your rights to work written entirely by you; rather, the intent is to
exercise the right to control the distribution of derivative or
collective works based on the Program.

In addition, mere aggregation of another work not based on the Program
with the Program (or with a work based on the Program) on a volume of
a storage or distribution medium does not bring the other work under
the scope of this License.

  3. You may copy and distribute the Program (or a work based on it,
under Section 2) in object code or executable form under the terms of
Sections 1 and 2 above provided that you also do one of the following:

    a) Accompany it with the complete corresponding machine-readable
    source code, which must be distributed under the terms of Sections
    1 and 2 above on a medium customarily used for software interchange; or,

    b) Accompany it with a written offer, valid for at least three
    years, to give any third party, for a charge no more than your
    cost of physically performing source distribution, a complete
    machine-readable copy of the corresponding source code, to be
    distributed under the terms of Sections 1 and 2 above on a medium
    customarily used for software interchange; or,

    c) Accompany it with the information you received as to the offer
    to distribute corresponding source code.  (This alternative is
    allowed only for noncommercial distribution and only if you
    received the program in object code or executable form with such
    an offer, in accord with Subsection b above.)

The source code for a work means the preferred form of the work for
making modifications to it.  For an executable work, complete source
code means all the source code for all modules it contains, plus any
associated interface definition files, plus the scripts used to
control compilation and installation of the executable.  However, as a
special exception, the source code distributed need not include
anything that is normally distributed (in either source or binary
form) with the major components (compiler, kernel, and so on) of the
operating system on which the executable runs, unless that component
itself accompanies the executable.

If distribution of executable or object code is made by offering
access to copy from a designated place, then offering equivalent
access to copy the source code from the same place counts as
distribution of the source code, even though third parties are not
compelled to copy the source along with the object code.

  4. You may not copy, modify, sublicense, or distribute the Program
except as expressly provided under this License.  Any attempt
otherwise to copy, modify, sublicense or distribute the Program is
void, and will automatically terminate your rights under this License.
However, parties who have received copies, or rights, from you under
this License will not have their licenses terminated so long as such
parties remain in full compliance.

  5. You are not required to accept this License, since you have not
signed it.  However, nothing else grants you permission to modify or
distribute the Program or its derivative works.  These actions are
prohibited by law if you do not accept this License.  Therefore, by
modifying or distributing the Program (or any work based on the
Program), you indicate your acceptance of this License to do so, and
all its terms and conditions for copying, distributing or modifying
the Program or works based on it.

  6. Each time you redistribute the Program (or any work based on the
Program), the recipient automatically receives a license from the
original licensor to copy, distribute or modify the Program subject to
these terms and conditions.  You may not impose any further
restrictions on the recipients' exercise of the rights granted herein.
You are not responsible for enforcing compliance by third parties to
this License.

  7. If, as a consequence of a court judgment or allegation of patent
infringement or for any other reason (not limited to patent issues),
conditions are imposed on you (whether by court order, agreement or
otherwise) that contradict the conditions of this License, they do not
excuse you from the conditions of this License.  If you cannot
distribute so as to satisfy simultaneously your obligations under this
License and any other pertinent obligations, then as a consequence you
may not distribute the Program at all.  For example, if a patent
license would not permit royalty-free redistribution of the Program by
all those who receive copies directly or indirectly through you, then
the only way you could satisfy both it and this License would be to
refrain entirely from distribution of the Program.

If any portion of this section is held invalid or unenforceable under
any particular circumstance, the balance of the section is intended to
apply and the section as a whole is intended to apply in other
circumstances.

It is not the purpose of this section to induce you to infringe any
patents or other property right claims or to contest validity of any
such claims; this section has the sole purpose of protecting the
integrity of the free software distribution system, which is
implemented by public license practices.  Many people have made
generous contributions to the wide range of software distributed
through that system in reliance on consistent application of that
system; it is up to the author/donor to decide if he or she is willing
to distribute software through any other system and a licensee cannot
impose that choice.

This section is intended to make thoroughly clear what is believed to
be a consequence of the rest of this License.

  8. If the distribution and/or use of the Program is restricted in
certain countries either by patents or by copyrighted interfaces, the
original copyright holder who places the Program under this License
may add an explicit geographical distribution limitation excluding
those countries, so that distribution is permitted only in or among
countries not thus excluded.  In such case, this License incorporates
the limitation as if written in the body of this License.

  9. The Free Software Foundation may publish revised and/or new versions
of the General Public License from time to time.  Such new versions will
be similar in spirit to the present version, but may differ in detail to
address new problems or concerns.

Each version is given a distinguishing version number.  If the Program
specifies a version number of this License which applies to it and "any
later version", you have the option of following the terms and conditions
either of that version or of any later version published by the Free
Software Foundation.  If the Program does not specify a version number of
this License, you may choose any version ever published by the Free Software
Foundation.

  10. If you wish to incorporate parts of the Program into other free
programs whose distribution conditions are different, write to the author
to ask for permission.  For software which is copyrighted by the Free
Software Foundation, write to the Free Software Foundation; we sometimes
make exceptions for this.  Our decision will be guided by the two goals
of preserving the free status of all derivatives of our free software and
of promoting the sharing and reuse of software generally.

                            NO WARRANTY

  11. BECAUSE THE PROGRAM IS LICENSED FREE OF CHARGE, THERE IS NO WARRANTY
FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE LAW.  EXCEPT WHEN
OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR OTHER PARTIES
PROVIDE THE PROGRAM "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED
OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  THE ENTIRE RISK AS
TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU.  SHOULD THE
PROGRAM PROVE DEFECTIVE, YOU ASSUME THE COST OF ALL NECESSARY SERVICING,
REPAIR OR CORRECTION.

  12. IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING
WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MAY MODIFY AND/OR
REDISTRIBUTE THE PROGRAM AS PERMITTED ABOVE, BE LIABLE TO YOU FOR DAMAGES,
INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING
OUT OF THE USE OR INABILITY TO USE THE PROGRAM (INCLUDING BUT NOT LIMITED
TO LOSS OF DATA OR DATA BEING RENDERED INACCURATE OR LOSSES SUSTAINED BY
YOU OR THIRD PARTIES OR A FAILURE OF THE PROGRAM TO OPERATE WITH ANY OTHER
PROGRAMS), EVEN IF SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE
POSSIBILITY OF SUCH DAMAGES.

                     END OF TERMS AND CONDITIONS

            How to Apply These Terms to Your New Programs

  If you develop a new program, and you want it to be of the greatest
possible use to the public, the best way to achieve this is to make it
free software which everyone can redistribute and change under these terms.

  To do so, attach the following notices to the program.  It is safest
to attach them to the start of each source file to most effectively
convey the exclusion of warranty; and each file should have at least
the "copyright" line and a pointer to where the full notice is found.

    &lt;one line to give the program's name and a brief idea of what it does.&gt;
    Copyright (C) &lt;year&gt;  &lt;name of author&gt;

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program; if not, write to the Free Software
    Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA


Also add information on how to contact you by electronic and paper mail.

If the program is interactive, make it output a short notice like this
when it starts in an interactive mode:

    Gnomovision version 69, Copyright (C) year name of author
    Gnomovision comes with ABSOLUTELY NO WARRANTY; for details type `show w'.
    This is free software, and you are welcome to redistribute it
    under certain conditions; type `show c' for details.

The hypothetical commands `show w' and `show c' should show the appropriate
parts of the General Public License.  Of course, the commands you use may
be called something other than `show w' and `show c'; they could even be
mouse-clicks or menu items--whatever suits your program.

You should also get your employer (if you work as a programmer) or your
school, if any, to sign a "copyright disclaimer" for the program, if
necessary.  Here is a sample; alter the names:

  Yoyodyne, Inc., hereby disclaims all copyright interest in the program
  `Gnomovision' (which makes passes at compilers) written by James Hacker.

  &lt;signature of Ty Coon&gt;, 1 April 1989
  Ty Coon, President of Vice

This General Public License does not permit incorporating your program into
proprietary programs.  If your program is a subroutine library, you may
consider it more useful to permit linking proprietary applications with the
library.  If this is what you want to do, use the GNU Library General
Public License instead of this License.
            
</pre>
    </div>
  </div>

  <div>
    <p class="footer">Copyright &Acirc;&copy; 2005-2008 Thomas Harding.<br>
    Copying and distribution of this article can be made under General Public
    License. see <a href="README">README</a> and <a href=
    "COPYING">COPYING</a>.</p>
  </div>
