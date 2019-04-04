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

Find every mp4 in folder, extract its name and convert it to mp3. 
```bash
ls | grep 'mp4' | sed -E 's/.mp4/\n/g' | sed -r '/^\s*$/d' | xargs -I@ bash -c "ffmpeg -i '@.mp4' -vn -acodec libmp3lame -ac 2 -ab 160k -ar 48000 '@.mp3'"
```

Show info on every commit in all branches. 
```bash
git rev-list --all --remotes | xargs -I@ bash -c "git show --pretty=format:'#%h %ae (%cD) %s'  --name-status @"
```

Base on the example above: show the most frequently updating file in repository. 
```bash
git rev-list --all --remotes | xargs -I@ bash -c "git show --pretty=format:''  --name-status @" | sort | uniq -c | sort -r | head -n 10
```

Almost the same but show only the most frequently updating file in current branch.
```bash
polpc03742:balance-deducting-service lukasz.czapski$ git log --pretty=format:%H --no-patch | xargs -I@ bash -c "git show --pretty=format:''  --name-status @" | sort | uniq -c | sort -r | head -n 10
```
