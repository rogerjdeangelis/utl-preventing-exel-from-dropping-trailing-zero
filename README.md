# utl-preventing-exel-from-dropping-trailing-zero
Preventing exel from dropping trailing zeros   
    Preventing exel from dropping trailing zeros                                                                                 
                                                                                                                                 
    SAS Form                                                                                                                     
    https://tinyurl.com/yykjf73f                                                                                                 
    https://communities.sas.com/t5/SAS-Programming/SAS-dataset-to-CSV-missing-trailing-zeros-in-character-variable/m-p/679738    
                                                                                                                                 
    SOAPBOX ON                                                                                                                   
      There are much more powerfull methods than 'proc export'.                                                                  
      Namely Python, R, SAS libname, sql passthru and connectio to excel.                                                        
    SOAPBOX OFF                                                                                                                  
                                                                                                                                 
    Problem                                                                                                                      
        When I use 'proc export' sas converts my character numerics to numeric and drop trailing zeros;                          
                                                                                                                                 
           d:/xls/trailzro.xlsx                                                                                                  
                 ____________                      ____________                                                                  
                 |   A      |                      |   A      |                                                                  
                 +----------+                      +----------+                                                                  
              1  |employy   |                   1  |employy   |                                                                  
                 |----------|  But I want this     |----------|                                                                  
              2  |1004.131 0|                   2  |1004.13100|                                                                  
                 |----------|                      |----------|                                                                  
              3  |1004.1314 |                   3  |1004.13140|                                                                  
                 |----------|                      |----------|                                                                  
              4  |1003.4562 |                   4  |1003.45620|                                                                  
                 ------------                      ------------                                                                  
             [zro]                             [zro]                                                                             
                                                                                                                                 
    data have;                                                                                                                   
       input  employy$10.;                                                                                                       
    cards4;                                                                                                                      
    1004.13100                                                                                                                   
    1004.13140                                                                                                                   
    1003.45620                                                                                                                   
    ;;;;                                                                                                                         
    run;quit;                                                                                                                    
                                                                                                                                 
    * SOLUTION;                                                                                                                  
                                                                                                                                 
    ods excel file="d:/xls/trailzro.xlsx" options(sheet_name="zro");                                                             
    proc report data=have nowd missing box;                                                                                      
    col employy;                                                                                                                 
    define employy / style={just=right tagattr='format:####.00000'};                                                             
    run;quit;                                                                                                                    
    ods excel close;                                                                                                             
                                                                                                                                 
    d:/xls/trailzro.xlsx                                                                                                         
          ____________                                                                                                           
          |   A      |                                                                                                           
          +----------+                                                                                                           
       1  |employy   |                                                                                                           
          |----------|                                                                                                           
       2  |1004.13100|                                                                                                           
          |----------|                                                                                                           
       3  |1004.13140|                                                                                                           
          |----------|                                                                                                           
       4  |1003.45620|                                                                                                           
          ------------                                                                                                           
      [zro]                                                                                                                      
                                                                                                                                 
