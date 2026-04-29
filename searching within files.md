# Grep 

text inside files 

grep "error" server.log
grep - n "error" server.log (shows line number)

grep -i "error" server.log (search case insensitive)

grep -rn "defaults"
grep -rnC 3 "defaults"

grep -E "error|warning"
