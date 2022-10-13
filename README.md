알고리즘 기록하는 브랜치

## 2022- 10 - 07
https://www.acmicpc.net/problem/14499

주사위를 입체적으로 어떻게 굴러갈지 생각하는게 중요

처음에 구현사항중 하나를 빼먹고 안봐서 오래걸림.
<details>
<summary>code</summary>
<div markdown="1">

```python

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
</div>
</details>


-----------------------------
https://www.acmicpc.net/problem/14500
이어진 두칸의 좌표를 방문처리하고 방문한 두점에서 각각 3방향을 체크하는 bfs를 실행하는것,
1자로된 테트리스 하나만 체크해주면 끝

<details>
<summary>code</summary>
<div markdown="1">
```python

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

</div>
</details>

## 2022 - 10 - 08

https://www.acmicpc.net/problem/14890
평범한 구현문제

위->아래로갈떄
아래->위로갈때 두가지 경우로 나눠서 발판을 놓는경우를 생각하면된다.

<details>
<summary>code</summary>
<div markdown="1">

```python

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
</div>
</details>
---------------------------------
## 2022 - 10 - 11

https://www.acmicpc.net/problem/16235

dict를 활용해서 다양한 정보를 저장해야 했던 구현문제
<details>
<summary>code</summary>
<div markdown="1">

```python

n,m,k = map(int,input().split(" "))
arr = []
for i in range(n):
    arr.append(list(map(int,input().split(" "))))
tree = []
treearr = {}
for i in range(m):
    tree = list(map(int,input().split(" ")))
    treearr[(tree[0]-1,tree[1]-1)]=[tree[2]]
dx = [0,0,1,-1,1,-1,1,-1]
dy = [1,-1,0,0,-1,1,1,-1]
temparr = [[5 for _ in range(n)] for _ in range(n)]
answer = 0
for i in range(k):
    change=[]
    savearr = treearr
    #print(treearr)
    for jdx,j in enumerate(savearr):
        treearr[j].sort()
        for kdx,k in enumerate(treearr[j]): #봄
            if temparr[j[0]][j[1]]<k:
                treearr[j][kdx]=-k
            elif temparr[j[0]][j[1]]>=k:
                #print("in")
                temparr[j[0]][j[1]]-=k
                treearr[j][kdx]+=1
        #print(treearr[j],"여름전",k)
        kdx = 0
        treelen = len(treearr[j])
        for k in range(treelen):
            k = treearr[j].pop(0)
            if k<0:
                temparr[j[0]][j[1]]+=(-k)//2
            else:
                treearr[j].append(k)
        #print(treearr,"가을전",k)
        for kdx, k in enumerate(treearr[j]):  # 가을
            if k%5==0 and k>0:
                for di in range(8):
                    if j[0]+dx[di]<0 or j[1]+dy[di]<0 or j[0]+dx[di]>=n or j[1]+dy[di]>=n:
                        continue
                    #print(j[0]+dx[di],j[1]+dy[di])
                    change.append([j[0]+dx[di],j[1]+dy[di]])
    for j in change: #가을값 변동
        try:
            treearr[j[0],j[1]].append(1)
        except KeyError:
            treearr[(j[0],j[1])]=[1]
    for j in range(n):  #겨울
        for k in range(n):
            temparr[j][k]+=arr[j][k]
    #if i==5:
        #print(treearr,temparr)
#print(treearr)
#print(temparr)
for i in treearr:
    answer+=len(treearr[i])

print(answer)
```
</div>
</details>

-------------------------
## 2022-10-12
https://www.acmicpc.net/problem/14503

평범한 구현문제

너무 꼬아서 생각해서 오래걸림

<details>
<summary>code</summary>
<div markdown="1">

```python

n,m = map(int,input().split(" "))
r,c,d = map(int,input().split(" "))
arr = []
for i in range(n):
    arr.append(list(map(int,input().split(" "))))
dx = [-1,0,1,0]
dy = [0,1,0,-1]
err = 0 #4방향다 못가는경우 체크
answer = 0
while 1:
    #1단계
    if arr[r][c]==0:
        arr[r][c]=2
        answer+=1
    if err == 4: #2-3 단계
        #print(r,c,d,err,"in")
        nx = r+dx[(d+2)%4]
        ny = c+dy[(d+2)%4]
        if arr[nx][ny]==1:
            break
        err=0
        r=nx #뒤로 한칸빠질수이쓰면 빠진다.
        c=ny
        err=0
        #print(r,c,d,err,"out")
        continue
    d = (d + 3) % 4
    nx = r+dx[d]
    ny = c+dy[d]

    if arr[nx][ny]==1 or arr[nx][ny]==2: #벽 or 이미청소
        err+=1
        continue
    elif arr[nx][ny]==0:  #청소가능
        #print(nx,ny,d)
        err=0
        r=nx
        c=ny
        continue
print(answer)


```
</div>
</details>

## 2022- 10 - 13

https://www.acmicpc.net/problem/17144

시간복잡도 줄이기위한 최적화가 어려웠음

<details>
<summary>code</summary>
<div markdown="1">
    
```python

import copy
r,c,t = map(int,input().split(" "))
arr = []
for i in range(r):
    arr.append(list(map(int,input().split(" "))))

machine = []
def updown(top):
    dx = [0, -1, 0, 1]
    dy = [1, 0, -1, 0]
    direct = 0
    before = 0
    x, y = top, 1
    while True:
        nx = x + dx[direct]
        ny = y + dy[direct]
        if x == top and y == 0:
            break
        if nx < 0 or nx >= r or ny < 0 or ny >= c:
            direct += 1
            continue
        arr[x][y], before = before, arr[x][y]
        x = nx
        y = ny
def updown2(top):
    dx = [0, 1, 0, -1]
    dy = [1, 0, -1, 0]
    direct = 0
    before = 0
    x, y = top, 1
    while True:
        nx = x + dx[direct]
        ny = y + dy[direct]
        if x == top and y == 0:
            break
        if nx < 0 or nx >= r or ny < 0 or ny >= c:
            direct += 1
            continue
        arr[x][y], before = before, arr[x][y]
        x = nx
        y = ny
for k in range(t):
    dx = [0, 0, 1, -1]
    dy = [1, -1, 0, 0]
    memarr = copy.deepcopy(arr)
    for i in range(r): #확산
        for j in range(c):
            if memarr[i][j]==-1 and machine == []:
                machine.append(i)
                machine.append(i+1)
            if memarr[i][j]>0: #미세먼지가 있으면
                for d in range(4):
                    nx = i+dx[d]
                    ny = j+dy[d]
                    num = memarr[i][j]//5
                    if 0<=nx<r and 0<=ny<c and memarr[nx][ny]!=-1:
                        arr[nx][ny]+=num
                        arr[i][j]-=num
    mx= machine[0]
    x =mx
    my = 0
    mx2 = machine[1]
    my2 = 0
    updown(mx)
    updown2(mx+1)
    #print(arr)
answer = 0
for i in range(r):  # 확산
    for j in range(c):
        if arr[i][j]>0:
            answer+=arr[i][j]
print(answer)

```
</div>
</details>
----------------------------

https://www.acmicpc.net/problem/21611

구현내용이 복잡해 어려웠다

<details>
<summary>code</summary>
<div markdown="1">
    
```python

import copy
n,m = map(int,input().split(" "))
arr = []
for i in range(n):
    arr.append(list(map(int,input().split(" "))))
blz = []
sx = n//2
sy = n//2
answer =[ 0,0,0]
def plus(memarr):
    queue = []
    temparr = []
    for i in memarr:
        if len(queue)!=0:
            if i == queue[-1]:
                queue.append(i)
            else:
                temparr.append(len(queue))
                temparr.append(queue[-1])
                queue.clear()
                queue.append(i)
        else:
            queue.append(i)
    if len(queue)!=0:
        temparr.append(len(queue))
        temparr.append(queue[-1])
    return temparr
def bomb(memarr):
    while 1:
        ck = 0
        queue = []
        tempmem = []
        while memarr!=[]:
            #print(memarr)
            num = memarr.pop(0)
            #print(queue,num)
            if len(queue)!=0:
                if queue[-1]!=num:
                    if len(queue)>=4:
                        answer[queue[-1]-1]+=len(queue)
                        ck = 1
                        tempmem.append(num)
                        queue.clear()
                    else:
                        #print(queue,num)
                        while queue!=[]:
                            tempmem.append(queue.pop())
                        queue.append(num)
                else:
                    queue.append(num)
            else:
                queue.append(num)
        #print(queue)
        if len(queue)!=0:
            if len(queue)<4:
                while queue != []:
                    tempmem.append(queue.pop())
            else:
                answer[queue[0]-1]+=len(queue)
        if ck==0:
            break
        #print(tempmem)
        memarr = tempmem
        #print(memarr)
    return tempmem
def spin(x,y,arr):
    memarr = []
    d=0
    leng = 1
    cnt = 0
    for i in range(n//2):
        for j in range(leng):
            y-=1
            if arr[x][y]!=0:
                memarr.append(arr[x][y])
        for j in range(leng):
            x+=1
            #print(x, y)
            if arr[x][y]!=0:
                memarr.append(arr[x][y])
        leng+=1
        for j in range(leng):
            y+=1
            if arr[x][y]!=0:
                memarr.append(arr[x][y])
        for j in range(leng):
            x-=1
            #print(arr[x][y], x, y)
            if arr[x][y]!=0:
                memarr.append(arr[x][y])
        leng+=1
    for j in range(leng-1):
        y-=1
        if arr[x][y] != 0:
            memarr.append(arr[x][y])
    leng= 1
    #print(memarr)
    memarr = bomb(memarr)
    #print(memarr)
    memarr = plus(memarr)
    #print(memarr)
    lenmem = len(memarr)  # memarr가지고 터지는곳 체크
    #print(memarr)
    x=sx
    y=sy
    temparr= [[0 for _ in range(n+1)] for _ in range(n+1)]
    if lenmem==0:
        return temparr
    for i in range(n//2):
        for j in range(leng):
            y-=1
            temparr[x][y]=memarr[cnt]
            cnt+=1
            if cnt==lenmem:
                return temparr
        for j in range(leng):
            x+=1
            temparr[x][y] = memarr[cnt]
            cnt += 1
            if cnt == lenmem:
                return temparr
        leng+=1
        for j in range(leng):
            y+=1
            temparr[x][y] = memarr[cnt]
            cnt += 1
            if cnt == lenmem:
                return temparr
        #print(temparr)
        for j in range(leng):
            x-=1
            #print(x, y)
            temparr[x][y] = memarr[cnt]
            cnt += 1
            if cnt >= lenmem:
                return temparr
        leng+=1
    for j in range(leng-1):
        y-=1
        temparr[x][y] = memarr[cnt]
        cnt += 1
        if cnt >= lenmem:
            return temparr
    return temparr
for i in range(m):
    blz.append(list(map(int,input().split(" "))))
for d,s in blz:
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]
    x=sx
    y=sy
    for i in range(s):
        x=x+dx[d-1]
        y=y+dy[d-1]
        if 0<=x<n and 0<=y<n:
            arr[x][y]=0
    arr = spin(sx,sy,arr) # 자리 당기기
    #print(arr)
print(answer[0]+answer[1]*2+answer[2]*3)




```
</div>
</details>



