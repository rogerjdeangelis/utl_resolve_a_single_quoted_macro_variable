# utl_resolve_a_single_quoted_macro_variable
Resolving a single quoted macro variable

    ```  Resolving a single quoted macro variable;                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  http://www.lexjansen.com/mwsug/2017/RF/MWSUG-2017-RF02.pdf                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  You need to resolve &folder and maintain the outer single quotes                                                                                             ```
    ```                                                                                                                                                               ```
    ```    Here is the problem, folder is not resolved inside single quotes.                                                                                          ```
    ```                                                                                                                                                               ```
    ```      %let folder=matlab;                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```      %let pth='dir "d:/program files/&folder/*.xls" /o:n /b';                                                                                                 ```
    ```                                                                                                                                                               ```
    ```      %put &=pth;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```      Folder is not resolved                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```      PTH='dir "d:/program files/&folder/*.xls" /o:n /b'                                                                                                       ```
    ```                                                                                                                                                               ```
    ```  Solution (This works and is the most readble and loagical?  quote/unquote)                                                                                   ```
    ```  You dont have to learn all those macro quoting functions?                                                                                                    ```
    ```                                                                                                                                                               ```
    ```     %let pth=%sysfunc(quote('dir "d:/program files/&folder/*.xls" /o:n /b'));                                                                                 ```
    ```                                                                                                                                                               ```
    ```     %put &=pth;                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```     PTH="'dir ""d:/program files/matlab/*.xls"" /o:n /b'"                                                                                                     ```
    ```                                                                                                                                                               ```
    ```     %put  pth = %sysfunc(dequote(&pth));                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```    Result                                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```     PTH ='dir "d:/program files/matlab/*.xls" /o:n /b'                                                                                                        ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  These do not work with existing single quotes.                                                                                                               ```
    ```  Also somewhat Klingon?                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```  Also beware of how SAS handles all the generated quoting special characters?                                                                                 ```
    ```                                                                                                                                                               ```
    ```     %let pth = %str(%'dir "d:/program files/&folder/*.xls" /o:n /b%');                                                                                        ```
    ```                                                                                                                                                               ```
    ```     %put &=pth;                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```     %let pth = %bquote(')dir "d:/program files/&folder/*.xls" /o:n b%bquote(');                                                                               ```
    ```                                                                                                                                                               ```
    ```     %put &=pth;                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```     %put %tslit(dir "c:\&temp\*.sas" /o:n /b);                                                                                                                ```
    ```                                                                                                                                                               ```
    ```  I could not get the following to work                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```    %let pth=%unquote(%bquote('dir "d:/program files/&folder/*.xls" /o:n'));                                                                                   ```
    ```                                                                                                                                                               ```
    ```    %put &=pth;                                                                                                                                                ```

