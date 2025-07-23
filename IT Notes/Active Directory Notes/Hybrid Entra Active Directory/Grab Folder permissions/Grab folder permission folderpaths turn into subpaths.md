Excel

=TRIM(SUBSTITUTE(A1:A1000,"\\kustom-fs1\",""))

##### Grab folder permissions folderpaths and just grab name without subpaths.txt
Excel

=TRIM(RIGHT(SUBSTITUTE(A1:A1600,"\",REPT(" ",LEN(A1))),LEN(A1)))