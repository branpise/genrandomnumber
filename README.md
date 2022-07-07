**Task 1**
```
Please design a script that writes the numbers from 1 - 10 in random order. 
Each number should appear only once. You can use bash only. 
Please provide tests for the script, along with documentation which should include 
the following: 
● Build instructions
● Usage
● Description
● Known limitations / bugs
```

**Solution:**

**Build Instructions**

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

**Output**
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
**Usage**
- Run the below commands to get the output of the bash script:
```
$ bash <script name>
$ bash genrandom.sh
```
- To run the same script in debug mode:
```
$ bash -x <script-name>
$ bash -x genrandom.sh
```
**Description**
```
- I used the ‘awk’ command to complete this activity. Here;
- Loop variable is initialized by 10 and the loop will terminate if the value=10.
- I defined ‘numb’ as the variable that will generate a random number and it will increment by ‘+1’ 
- And will multiply by the defined range which is, Range=10.
- This same number will be incremented by 1.
- It will run a while loop over the count variable until the loop ends.
```
**Known limitations / bugs**
```
N/A
```

**Task 2**
```
Imagine a server with the following specs: 
● 4 times Intel(R) Xeon(R) CPU E7-4830 v4 @ 2.00GHz
● 64GB of ram
● 2 tb HDD disk space
● 2 x 10Gbit/s nics
The server is used for SSL offloading and proxies around 25000 requests per second. 
Please let us know which metrics are interesting to monitor in that specific case and 
how would you do that? What are the challenges of monitoring this? 
```

**Solution:**
```
The problem statement shows that there are 25000 requests per second that the server is processing for the SSL off loading, which is huge, high IO wait, etc.
The first and foremost task would be to monitor the hardware resources like: CPU usage, Memory , disk utilization. 
We will need to keep a watch on the metrics like upload/download speed on the NIC cards, transmission speed, etc.
With the use of 'top' command we can monitor the real time CPU utilization whic shows the average load along with '%CPU' and '%MEM' utilization.
We can also use 'lscpu -e' we can check the number of cores and the caches shared on the server.
For memory we can use 'cat /proc/meminfo' which will show you the total memory along with the free, buffer, cache.
'free -m' can also be used to monitor memory. To check processes, block IO, CPU activity we can also make use of 'vmstat' command.
For disk we can use the 'iotop -o' command which will provide the realtim disk activity along with the processes that are performing IO.
'iostat' command would also help in collecting the disk statistics, for example we can use 'iostat -y 5' command to display each report every 5 seconds, including the CPU stats and the disk stats.

If we see the latency or we notice that the hardware resources are overutilized then we have two approaches:
- Either to increase the hardware if that is possible.
- If not the first option, then we will have to put limitation to the apache server to process the certain amount of requests.
```


