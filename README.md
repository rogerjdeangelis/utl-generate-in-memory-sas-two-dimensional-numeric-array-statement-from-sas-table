# utl-generate-in-memory-sas-two-dimensional-numeric-array-statement-from-sas-table
Generate in memory sas two dimensional numeric array statement from sas table
    %let pgm=utl-generate-in-memory-sas-two-dimensional-numeric-array-statement-from-sas-table;

    %stop_submission;

    Generate in memory sas two dimensional numeric array statement from sas table

    CONTENTS

        1 get array from sas table (generate this code segment "[3,3] ( 11,12,13,21,22,23,31,32,33 )" )
        2 log
        3 utl_getary macro

    github
    https://tinyurl.com/vfffx6zd
    https://github.com/rogerjdeangelis/utl-generate-in-memory-sas-two-dimensional-numeric-array-statement-from-sas-table

    PROBLEM

      Sum the values along the main diagonal(the trace)
      have[1,1]+have[2,2]+have[3,3]

      NOTE: Solution works non square tables

    /**************************************************************************************************************************/
    /* INPUT                     | PROCESS                                   | OUTPUT (COMPUTE SUM OF MAIN DIAGONAL)          */
    /* =====                     | =======                                   | ======                                         */
    /* HAVE1 HAVE2 HAVE3         | 1 GET ARRAY FROM SAS TABLE (NOTE NO INPUT)| have[1,1]+have[2,2]+have[3,3]                  */
    /*                           | ==========================                |                                                */
    /*   11    12    13          |                                           |    11 +      22 +      33  =66                 */
    /*   21    22    23          | data want;                                |                                                */
    /*   31    32    33          |   array have %utl_getary(have);           | trace=66                                       */
    /*                           |   trace=have[1,1]+have[2,2]+have[3,3];    |                                                */
    /* data have;                |   put trace=;                             | WORK.WANT total obs=1                          */
    /* input have1               |   keep trace;                             |  TRACE                                         */
    /*  have2                    | run;quit;                                 |    66                                          */
    /* have3;  ;                 |                                           |                                                */
    /* cards4;                   |                                           |                                                */
    /* 11 12 13                  | 2 LOG SEE BELOW                           | ARRAY_STR=[3,3] ( 11,12,13,21,22,23,31,32,33 );*/
    /* 21 22 23                  |                                           |                                                */
    /* 31 32 33                  |                                           |                                                */
    /* ;;;;                      | 3 UTL_GETARY SEE BELOW                    |                                                */
    /* run;quit;                 |                                           |                                                */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data have;
    input have1
     have2
    have3;  ;
    cards4;
    11 12 13
    21 22 23
    31 32 33
    ;;;;
    run;quit;


    /**************************************************************************************************************************/
    /*   WORK.HAVE total obs=3     |  WHAT WE WANT TO DO                                                                      */
    /*                             |                                                                                          */
    /*   HAVE1    HAVE2    HAVE3   |  have[1,1]+have[2,2]+have[3,3]                                                           */
    /*                             |                                                                                          */
    /*     11       12       13    |     11 +      22 +      33  =  66                                                        */
    /*     21       22       23    |                                                                                          */
    /*     31       32       33    |                                                                                          */
    /**************************************************************************************************************************/

    /*              _                                   __                                      _        _     _
    / |   __ _  ___| |_    __ _ _ __ _ __ __ _ _   _   / _|_ __ ___  _ __ ___   ___  __ _ ___  | |_ __ _| |__ | | ___
    | |  / _` |/ _ \ __|  / _` | `__| `__/ _` | | | | | |_| `__/ _ \| `_ ` _ \ / __|/ _` / __| | __/ _` | `_ \| |/ _ \
    | | | (_| |  __/ |_  | (_| | |  | | | (_| | |_| | |  _| | | (_) | | | | | |\__ \ (_| \__ \ | || (_| | |_) | |  __/
    |_|  \__, |\___|\__|  \__,_|_|  |_|  \__,_|\__, | |_| |_|  \___/|_| |_| |_||___/\__,_|___/  \__\__,_|_.__/|_|\___|
         |___/                                 |___/
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %deletesasmacn;
    %symdel ary / nowarn;

    %put %utl_getary(have);

    data want;
      array have %utl_getary(have);
      trace=have[1,1]+have[2,2]+have[3,3];
      put trace=;
    run;quit;

    /***************************************************|*******************************************/
    /*| ARRAY_STR=[3,3] ( 11,12,13,21,22,23,31,32,33 ); |                                          */
    /*|                                                 | have[1,1]+have[2,2]+have[3,3]            */
    /*| WORK.WANT total obs=1                           |                                          */
    /*|  TRACE                                          |    11 +      22 +      33  =66           */
    /*|    66                                           |                                          */
    /***********************************************************************************************/

    /*___    _
    |___ \  | | ___   __ _
      __) | | |/ _ \ / _` |
     / __/  | | (_) | (_| |
    |_____| |_|\___/ \__, |
                     |___/
    */

    751     array have %utl_getary(have);
    MLOGIC(UTL_GETARY):  Beginning execution.
    MLOGIC(UTL_GETARY):  Parameter DSN has value have
    MLOGIC(UTL_GETARY):  %SYMDEL  ARY/NOWARN
    MLOGIC(DOSUBL):  Beginning execution.
    MLOGIC(DOSUBL):  This macro was compiled from the autocall file c:\oto\dosubl.sas
    MLOGIC(DOSUBL):  %LET (variable name is RC)
    SYMBOLGEN:  Macro variable ARG resolves to '%symdel ary/nowarn;data _null_;  set &dsn end=eof;
     array vars[*] _numeric_;  length allvals $32756;  length array_str $32756;
                 length prefix $44;  retain allvals;  length temp $32;  do i = 1 to dim(vars);
    temp = strip(put(vars[i], best32.));    if missing(allvals) then allvals =
                temp;    else allvals = catx(",", allvals, temp);  end;  if eof then do;    r = _n_;
    c = dim(vars);    prefix = cats("[",r,",",c,"] (");    suffix = ");";
                  array_str = catx(" ",prefix,allvals,suffix);    put array_str=;
    call symputx("ary",array_str);  end;run;quit;'
    SYMBOLGEN:  Macro variable DSN resolves to have
    ARRAY_STR=[3,3] ( 11,12,13,21,22,23,31,32,33 );
    NOTE: There were 3 observations read from the data set WORK.HAVE.
    NOTE: DATA statement used (Total process time):
          real time           0.00 seconds
          user cpu time       0.00 seconds
          system cpu time     0.00 seconds
          memory              1427.25k
          OS Memory           24056.00k
          Timestamp           08/01/2022 02:24:32 PM
          Step Count                        156  Switch Count  0


    MLOGIC(DOSUBL):  Ending execution.
    SYMBOLGEN:  Macro variable ARY resolves to [3,3] ( 11,12,13,21,22,23,31,32,33 );
    MPRINT(UTL_GETARY):   [3,3] ( 11,12,13,21,22,23,31,32,33 );
    MLOGIC(UTL_GETARY):  Ending execution.
    752     trace=have[1,1]+have[2,2]+have[3,3];
    753     put trace=;
    754   run;

    TRACE=66

    /*____         _   _                _
    |___ /   _   _| |_| |     __ _  ___| |_ __ _ _ __ _   _
      |_ \  | | | | __| |    / _` |/ _ \ __/ _` | `__| | | |
     ___) | | |_| | |_| |   | (_| |  __/ || (_| | |  | |_| |
    |____/   \__,_|\__|_|____\__, |\___|\__\__,_|_|   \__, |
                       |_____|___/                    |___/
    */



    /*--- all the deletes because   ---*/
    /*--- poor dosubl documentation ---*/

    filename ft15f001 "c:/oto/utl_getary.sas";
    parmcards4;
    %macro utl_getary(dsn);
    %symdel ary/nowarn;
    %dosubl('
    %symdel ary/nowarn;
    data _null_;
      set &dsn end=eof;
      array vars[*] _numeric_;
      length allvals $32756;
      length array_str $32756;
      length prefix $44;
      retain allvals;
      length temp $32;
      do i = 1 to dim(vars);
        temp = strip(put(vars[i], best32.));
        if missing(allvals) then allvals = temp;
        else allvals = catx(",", allvals, temp);
      end;
      if eof then do;
        r = _n_;
        c = dim(vars);
        prefix = cats("[",r,",",c,"] (");
        suffix = ");";
        array_str = catx(" ",prefix,allvals,suffix);
        put array_str=;
        call symputx("ary",array_str);
      end;
    run;quit;
    ')
    &ary
    %mend utl_getary;
    ;;;;
    run;quit;


    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
