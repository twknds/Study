알고리즘 기록하는 브랜치

2022- 10 - 07
https://www.acmicpc.net/problem/14499

주사위를 입체적으로 어떻게 굴러갈지 생각하는게 중요

처음에 구현사항중 하나를 빼먹고 안봐서 오래걸림.

```
n,m,x,y,k = map(int,input().split(" "))
arr = []
for i in range(n):
    arr.append(list(map(int,input().split(" "))))
karr = list(map(int,input().split(" ")))

dice = [0,0,0,0,0,0]
bot = 1
for i in karr:
    if i == 3:
        x-=1
        if x<0:
            x+=1
            continue
        temp = dice[bot]
        dice[1] = dice[0]
        dice[0] = dice[3]
        dice[3] = dice[2]
        dice[2] = temp
        if arr[x][y]==0:
            arr[x][y]=dice[bot]
        else:
            dice[bot]=arr[x][y]
            arr[x][y]=0
    if i == 4:
        x+=1
        if x>=n:
            x-=1
            continue
        temp = dice[bot]
        dice[1] = dice[2]
        dice[2] = dice[3]
        dice[3] = dice[0]
        dice[0] = temp
        if arr[x][y] == 0:
            arr[x][y] = dice[bot]
        else:
            dice[bot] = arr[x][y]
            arr[x][y] = 0
    if i==1:
        y+=1
        if y>=m:
            y-=1
            continue
        temp = dice[bot]
        dice[1]=dice[5]
        dice[5]=dice[3]
        dice[3]=dice[4]
        dice[4]=temp
        if arr[x][y] == 0:
            arr[x][y] = dice[bot]
        else:
            dice[bot] = arr[x][y]
            arr[x][y] = 0
    if i==2:
        y -= 1
        if y<0:
            y+=1
            continue
        temp = dice[bot]
        dice[1] = dice[4]
        dice[4] = dice[3]
        dice[3] = dice[5]
        dice[5] = temp
        if arr[x][y] == 0:
            arr[x][y] = dice[bot]
        else:
            dice[bot] = arr[x][y]
            arr[x][y] = 0
    print(dice[3])
    #print(dice,dice[3],[x,y])


```
-----------------------------
https://www.acmicpc.net/problem/14500
이어진 두칸의 좌표를 방문처리하고 방문한 두점에서 각각 3방향을 체크하는 bfs를 실행하는것,
1자로된 테트리스 하나만 체크해주면 끝

```
dx = [0,0,1,-1]
dy = [1,-1,0,0]
n,m = map(int,input().split(" "))
def garo(x,y):
    sum = arr[x][y]+arr[x][y+1]
    arr1 = []
    for i in range(4):
        nx = x+dx[i]
        ny = y+dy[i]
        nx2 = x+dx[i]
        ny2 = y+dy[i]+1
        if i!=0:
            if nx>=0 and ny>=0 and nx<n and ny<m:
                arr1.append(arr[nx][ny])
        if i!=1:
            if nx2>=0 and ny2>=0 and nx2<n and ny2<m:
                arr1.append(arr[nx2][ny2])
    arr1.sort(reverse=True)
    #print(arr1,sum)
    return sum+arr1[0]+arr1[1]
def sero(x, y):
    sum = arr[x][y] + arr[x+1][y]
    arr1 = []
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        nx2 = x + dx[i]+1
        ny2 = y + dy[i]
        if i != 2:
            if nx >= 0 and ny >= 0 and nx < n and ny < m:
                arr1.append(arr[nx][ny])
        if i != 3:
            if nx2 >= 0 and ny2 >= 0 and nx2 < n and ny2 < m:
                arr1.append(arr[nx2][ny2])
    arr1.sort(reverse=True)
    return sum+arr1[0]+arr1[1]
def garo2(x,y):
    sum = arr[x][y]+arr[x][y+1]+arr[x][y+2]
    arr1 = []
    for i in range(4):
        nx = x+dx[i]
        ny = y+dy[i]
        nx2 = x+dx[i]
        ny2 = y+dy[i]+2
        if i!=0:
            if nx>=0 and ny>=0 and nx<n and ny<m:
                arr1.append(arr[nx][ny])
        if i!=1:
            if nx2>=0 and ny2>=0 and nx2<n and ny2<m:
                arr1.append(arr[nx2][ny2])
    arr1.sort(reverse=True)
    #print(arr1,sum)
    return sum+arr1[0]
def sero2(x, y):
    sum = arr[x][y] + arr[x+1][y] + arr[x+2][y]
    arr1 = []
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        nx2 = x + dx[i]+2
        ny2 = y + dy[i]
        if i != 2:
            if nx >= 0 and ny >= 0 and nx < n and ny < m:
                arr1.append(arr[nx][ny])
        if i != 3:
            if nx2 >= 0 and ny2 >= 0 and nx2 < n and ny2 < m:
                arr1.append(arr[nx2][ny2])
    arr1.sort(reverse=True)
    #print(arr1)
    return sum+arr1[0]

arr = []
for i in range(n):
    temp = list(map(int,input().split(" ")))
    arr.append(temp)
#print(arr)
answer = -1
for i in range(n):
    for j in range(m):
        if j!=m-1:
            answer = max(answer,garo(i,j))
            #print(i,j,answer,"garo")
        if i!=n-1:
            answer = max(answer,sero(i, j))
            #print(i, j, answer,"sero")
        if j<m-2:
            answer = max(answer,garo2(i,j))
            #print(i,j,answer,"garo2")
        if i<n-2:
            answer = max(answer,sero2(i, j))
            #print(i, j, answer,"sero2")
print(answer)
```

2022 - 10 - 08

https://www.acmicpc.net/problem/14890
평범한 구현문제

위->아래로갈떄
아래->위로갈때 두가지 경우로 나눠서 발판을 놓는경우를 생각하면된다.
```
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


