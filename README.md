# Useful tips

## CMD
Find given phrase in file and count the number of its occurrences.

```bash
cat file.2018-02-02.log | grep 'phrase' | wc -l
```

Find line in file with "Handling endpoint" and "Host". Than extract address for this host as second part in sed. Cut this part after ','. Sort this and count their occurrences.
```bash
cat file.log | grep 'endpoint' | grep 'Host' | sed -E  's/(.*)Host=(.*)/\2/' | cut -d',' -f1 | sort | uniq -c
```

List files except given pattern. Than remove this files. 
```bash
 ls | grep -v 2018-02-07 | xargs rm
```

Split large file into parts (by 1000000 lines). 
```bash
 split -l 1000000 big.log part_
```

Print evry 1000000 line start from 1 line. 
```bash
 sed -n '1p;0~1000000p' big.log 
```
