## 题目
https://www.youtube.com/watch?v=3Q_oYDQ2whs
![image](https://user-images.githubusercontent.com/43141076/137413830-bd0233a8-1afa-4656-bce8-16408dd30346.png)


## 解答

总体思路还是比较清楚的，可以分为以下几个步骤：

1. 对于会议：先把两个人的meeting合在一起，并且merge掉重复的部分；
2. 对于工作时间：取两人开工时间的较晚值作为开工时间，取两人下班时间的较早值作为下班时间；
3. 求工作时间和会议时间的差集；
4. 另外需要把string类型的时间转换成int，这样方便比较。结果确定后再转回去。

这题每一步都不是很难，但是想顺畅地衔接，以及不出bug的话，还是很考验基本功的。

另外第3步也比较tricky，感觉很容易出bug。因为最早的会议时间和最晚的会议时间都可能在工作时间之外。处理起来有点复杂。

比较好的解决办法是，把不能工作的时间，用“伪会议”来代替。即假设24小时都可以工作，但是首尾各插进去两个会议。

这样在merge完会议后，只需保存这些会议之间的gap，就可以得到需要的结果。

代码如下：


### helper functions
```
def time_to_int(times):
    for i in range(len(times)):
        for j in range(len(times[i])):
            hour, minute = times[i][j].split(":")
            times[i][j] = 60 * int(hour) + int(minute)
            
def int_to_time(times):
    for i in range(len(times)):
        for j in range(len(times[i])):            
            hour, minute = (times[i][j] // 60), times[i][j] % 60
            hour = str(hour) if hour else "00"
            minute = str(minute) if minute else "00"
            times[i][j] = hour + ":" + minute
            
def work_time_to_meeting(time):
    meetings = []
    meetings.append(["00:00", time[0]])
    meetings.append([time[1], "24:00"])
    return meetings
            
def merge_meeting(meetings):
    sorted_meetings = sorted(meetings, key=lambda x: x[0])
    res = []
    for meeting in sorted_meetings:
        if not res or meeting[0] > res[-1][1]:
            res.append(meeting)
        else:
            res[-1][1] = max(res[-1][1], meeting[1])
    return res
```

### main function
```
def find_free_time(cal1, working1, cal2, working2):
    booked1 = work_time_to_meeting(working1)
    booked2 = work_time_to_meeting(working2)
    meetings = cal1 + cal2 + booked1 + booked2
    time_to_int(meetings)
    
    merged_meeting = merge_meeting(meetings)
    
    res = []
    
    for i in range(1, len(merged_meeting)):
        start = merged_meeting[i-1][1]
        end = merged_meeting[i][0]
        res.append([start, end])
    
    int_to_time(res)
    return res
```

### test
```
calendar1 = [['9:00','10:30'],['12:00','13:00'],['16:00','18:00']]
working_time1 = ['9:00', '20:00']
calendar2 = [['10:00','11:30'],['12:30','14:30'],['14:30','15:00'],['16:00','17:00']]
working_time2 = ['10:00', '18:30']

find_free_time(calendar1, working_time1, calendar2, working_time2)
```
