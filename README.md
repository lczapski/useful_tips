# Useful tips

## CMD
Find given phrase in file and count the number of its occurrences.

```bash
cat file.2018-02-02.log | grep 'phrase' | wc -l
```

Find line in file with "Handling endpoint" and "Host". Than extract address for this host as second part in sed. Cut this part after ','. Sort this and count their occurrences.
```bash
cat file.2018-02-02.log | grep "Handling endpoint" | grep 'Host' | sed -E  's/(.*)Host=(.*)/\2/' | cut -d',' -f1 | sort | uniq -c
```
