https://www.youtube.com/watch?v=3Q_oYDQ2whs
![image](https://user-images.githubusercontent.com/43141076/137413830-bd0233a8-1afa-4656-bce8-16408dd30346.png)

在merge meetings之后，需要把bounds和meeting取差集。

还有一种办法，是用在首尾插入会议，作为bound。

```
def time_to_int(times):
    for i in range(len(times)):
        for j in range(len(times[i])):
            #print(times[i][j])
            hour, minute = times[i][j].split(":")
            times[i][j] = 60 * int(hour) + int(minute)
            
def int_to_time(times):
    for i in range(len(times)):
        for j in range(len(times[i])):            
            hour, minute = (times[i][j] // 60), times[i][j] % 60
            hour = str(hour) if hour else "00"
            minute = str(minute) if minute else "00"
            times[i][j] = hour + ":" + minute
            
            
def merge_meeting(meeting1, meeting2):
    sorted_meetings = sorted(meeting1 + meeting2, key=lambda x: x[0])
    res = []
    for meeting in sorted_meetings:
        if not res or meeting[0] > res[-1][1]:
            res.append(meeting)
        else:
            res[-1][1] = max(res[-1][1], meeting[1])
    return res

def merge_working(time1, time2):
    start = max(time1[0], time2[0])
    end = min(time1[1], time2[1])
    if start >= end:
        return []
    else:
        return [start, end]
def find_free_time(cal1, working1, cal2, working2):
    time_to_int(cal1)
    time_to_int([working1])
    time_to_int(cal2)
    time_to_int([working2])
    
    merged_meeting = merge_meeting(cal1, cal2)

    merged_working = merge_working(working1, working2)
    
    if not merged_working:
        return []
    
    start, end = merged_working
    res = []
    for meeting in merged_meeting:
        meeting_start, meeting_end = meeting
        if meeting_start <= end and start < meeting_start:
            res.append([start, meeting_start])
            start = meeting_end
        else:
            start = max(start, meeting_end)
    if start < end:
        res.append([start, end])
    
    int_to_time(res)
    return res    
```

```
calendar1 = [['9:00','10:30'],['12:00','13:00'],['16:00','18:00']]
working_time1 = ['9:00', '20:00']
calendar2 = [['10:00','11:30'],['12:30','14:30'],['14:30','15:00'],['16:00','17:00']]
working_time2 = ['10:00', '18:30']

find_free_time(calendar1, working_time1, calendar2, working_time2)
```
