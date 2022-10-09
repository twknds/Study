알고리즘 기록하는 브랜치

2022 - 10 - 08

https://www.acmicpc.net/problem/14890

```python```
n,l = map(int,input().split(" "))

arr = []
for i in range(n):
    arr.append(list(map(int,input().split(" "))))
def check(x):
    sum = 2
    mem = arr[x][0]
    mem2 = arr[0][x]
    lck =  0
    lck2 = 0
    err = 0
    err2 = 0
    for i in range(n):
        if arr[x][i]==mem:
            lck+=1
        elif abs(arr[x][i]-mem)>1:
            err=1
        elif arr[x][i]!=mem:
            if arr[x][i]>mem:
                if lck<l:
                    err=1
                    mem=11
                elif lck>=l:
                    mem = arr[x][i]
                lck = 1
            else:
                mem = arr[x][i]
                if i+l>n:
                    err=1
                else:
                    for j in range(i+1,i+l):
                        if mem!=arr[x][j]:
                            err=1
                            break
                    if err!=1:
                        lck=1-l
        if arr[i][x]==mem2:
            lck2+=1
        elif abs(arr[i][x]-mem2)>1:
            err2=1
        elif arr[i][x]!=mem2:
            if arr[i][x]>mem2:
                if lck2 < l:
                    err2 = 1
                    mem2=11
                elif lck2 >= l:
                    mem2 = arr[i][x]
                lck2 = 1
            else:
                mem2 = arr[i][x]
                if i+l>n:
                    err2=1
                else:
                    for j in range(i+1,i+l):
                        if mem2!=arr[j][x]:
                            err2=1
                            break
                    if err2!=1:
                        lck2=1-l
        #print(arr[i][x], mem2, lck2, err2, [i, x])
        #print(arr[x][i], mem, lck, err, [x, i])
    #print(err,err2,x)
    return sum-err-err2
answer = 0
for i in range(n):
    answer += check(i)
print(answer)
```
