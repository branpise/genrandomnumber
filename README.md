# genrandomnumber

```
awk -v loop=10 -v range=10 'BEGIN{
  srand()
  do {
    numb = 1 + int(rand() * range)
    if (!(numb in prev)) {
       print numb
       prev[numb] = 1
       count++
    }
  } while (count<loop)
}'
```
```
root@baremetal:/tmp# sh 2.sh
10
4
9
6
8
3
7
2
5
1
root@baremetal:/tmp#
```
