# utl_compile_time_or_execution_time_macro_quoting_function
Compile time or execution time macro quoting function. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Compile time or execution time macro quoting function

    github
    https://tinyurl.com/y7v982ff
    https://github.com/rogerjdeangelis/utl_compile_time_or_execution_time_macro_quoting_function

    SAS Forum
    https://tinyurl.com/ya8js3a9
    https://communities.sas.com/t5/Base-SAS-Programming/compile-time-or-execution-time-macro-quoting-function/m-p/446604

    Understanding the phases of the SAS interpreter/compiler can page huge dividends,
    especially in relation to DOSUBL. Hopefully SAS will provide more
    documentation on DOSUBL.

    Evaluating a macro expression during each phase of the SAS interpreter/compiler

      1. Delay evaluation during macro compilation.
      2. Evaluate the expression during macro compilation.
      3. Delay evaluation during datastep compilation.
      4. Evaluate the expression during datastep compilation.
      5. Evaluate the expression during datastep execution.

    INPUT
    =====

      %let xpr='1+1';


    PROCESS (All the code)
    ======================
       %utlnopts;

       %put 1. Delay evaluation during macro compilation;
       %let x=&par;
       %put &=x;
       run;quit;

       * TOT='1+1' ;


       %put 2. Evaluate the expression during macro compilation;
       %let x = %eval(%sysfunc(dequote(&par)));
       %put &=x;
       run;quit;

       * TOT=2 ;


       data _null_;
         x = &par;
         put '3. Delay evaluation during datastep compilation';
         put x=;
       run;quit;

       * X=1+1;

       data _null_;
         x = %eval(%sysfunc(dequote(&par)));
         put '4. Evaluate the expression during datastep compilation';
         put x=;
         run;quit;

       * X=2;

       data _null_;
         call symputx('arg',&par);
         put  '5. Evaluate the expression during datastep execution';
         rc=dosubl("
            data _null_;
              x=&arg;
              put x=;
            run;quit;
         ");
       run;quit;

       * X=2;

    OUTPUT
    ======

    1. Delay evaluation during macro compilation
       X='1+1'

    2. Evaluate the expression during macro compilation
       X=2

    3. Delay evaluation during datastep compilation
       X=1+1

    4. Evaluate the expression during datastep compilation
       X=2

    5. Evaluate the expression during datastep execution
       X=2


