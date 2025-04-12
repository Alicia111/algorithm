# 1. 什麼是複雜度 ＆ 我知道這個又能幹嘛

### 由於程式碼不是填空題，所以一個問題通常有很多種解法以及一個理論上的最佳解，而最佳解通常對電腦的負擔最低。

### 而複雜度簡單來說就是就是執行一個程式所需要的資源，~~現在對看到這篇的人來說唯一用處就是讓你的 leetcode 成績好看一點~~。

#### <font color='#dc0051'>註：以下內容會與演算法跟資料結構產生極大的關聯。 </font>

舉個栗子，leetcode第一題的兩數和：


```python
### 雙迴圈寫法
nums=[2,11,7,18]
target=9
List=[]
for i in range(len(nums)):
    for j in range(i+1,len(nums)):
        if nums[i] + nums[j] == target:
            List.append(i)
            List.append(j)
            break
print(List)
```


```python
### 字典寫法
nums=[2,11,7,18]
target=9
List=[]

check={}

for i in range(len(nums)):
    found = target-nums[i]
    if found in check:
        List.append(check[found])
        List.append(i)
        break
    else:
        check[nums[i]]=i
        
print(List)
```

# 2. 時間複雜度 

## 2.1 時間複雜度是什麼

### wiki上是這樣寫的，時間複雜度是一個函式，定義該演算法的執行時間。
### 所以顧名思義就是執行一個程式所需要的時間，我現在完全搞懂了， <font color='red'> 完全沒搞懂.jpg</font>。

拿出另外一個栗子：  
假設你今天裝好了一台 Ryzen 7 9800X3D 跟 RTX 5090 加 DDR5 64GB記憶體的電腦，你覺得跟你手上一開機就把空間變成直升機停機坪一樣的文書機哪個速度比較快。

先別難過，前人已經幫你定義好了一個方法，直接拿來用就好了。


```python
### 來確認一下吧

def Func1(nums:int):
    count=0
    for i in range(nums):
        for j in range(nums):
            count+=1
    return count

def Func2(nums:int):
    count=0
    for i in range(0,nums,2):
        count+=1

    return count

def Func3(nums:int):
    count=0
    for i in range(nums):
        count+=1
    return count

result1=Func1(10)
result2=Func2(10)
result3=Func3(10)

print('下述三條 for 循環了幾次')

ans1 = int(input('Func1執行次數：'))
print(f'{"正確" if ans1==result1 else "錯誤"}')

ans2 = int(input('Func2執行次數：'))
print(f'{"正確" if ans2==result2 else "錯誤"}')

ans3 = int(input('Func3執行次數：'))
print(f'{"正確" if ans3==result3 else "錯誤"}')
    

```

## 2.2 Big O 表示法
### 前人們將時間複雜度的函式定義為 O(y) ，其中y為次數，常見有：N、N<sup>2</sup>、logN 等。

### 相信從上面的程式你大概可以看出來：
### &emsp;Func1執行 10x10 / N * N = N<sup>2</sup> 次
### &emsp;Func2執行 10÷2次 /  Ｎ ÷ 2次
### &emsp;Func3執行 10次 / N 次

### 照理來說 Func2 跟 Func3 的時間複雜度為 O(N/2) 跟 O(N) 對吧，<font color='red'>那你又錯了</font>。
### 由於 Big O 只是讓你粗略估計次數而已，故有有以下幾點需要注意：
### &emsp; 1. 只留最高項的項數
### &emsp;2. 將係數簡化為1
#### 故實際執行 O(N/2) 次需簡化為 <bold>O(N)</bold>； O(27N<sup>8</sup>+ 12N<sup>4</sup>+ 28) 簡化為 O(N<sup>8</sup>)；O(100) 次需簡化為 O(1)。


這時候你大概會有一個問題就是：我的for迴圈裡面有break啊這樣還算我 O(N) 喔，這群科學家怎麼判的。先別把你的編譯器刪了，因為 Big O 的原理是判斷你的程式最多要執行幾次才算，例如說你要的目標在迴圈最後一個的話你寫了break也派不上用場。



## 2.3 常見的時間複雜度

### 相信修過資料結構的人接下來不是很熟悉就是很痛苦。

### 2.3-1 O(1)

#### O(1) 基本上是最簡單易懂的複雜度了，所以基本上不需要特殊的演算法，<font color='red'>只要有看到明確的數字就是 O(1) 。</font>
#### 四則運算、賦予變數值、取特定list項（ list[2] )

#### ~~當然除非是要考你不然基本遇不到 O(1) 的程式~~


```python
### O(1)的程式碼
def o1(nums:int):
    list = []
    for i in range(327):
        list.append(i)
    print(list[41])
o1(input('O(1)測試：'))
```

### 2.3-2 O (N)
#### O(N) 顧名思義就是根據變數的值執行次數，<b>一定要有一個從 1 到 N 的遍歷</b>
#### For 迴圈、list.index() 都算是執行N次

#### 大部分你在學期間遇到的程式都是 Ｏ(N)


```python
### O(N) 的程式碼
def oN(nums,target):
    list=[]
    times=0
    for i in range(nums):
        list.append(i)
        times+=
    while target>nums:
        target=int(input((f'請重新輸入:')))
                
    print(list.index(target))

num=int(input(f'輸入範圍：'))
target=int(input(f'輸入查找目標'))
oN(num,target)

```

### 2.3-3 O(N<sup>n</sup>) ，n表常數

#### 基於O(N) 的邏輯，加上更多重複遍歷

~~如果你大部分都只能寫出O(N<sup>N</sup>)的程式的話，那你還是別寫了~~


```python
### O(N^N)的程式碼

def complex(nums:int):
    times=0
    check=nums
    while check>0:
        for i in range(nums):
            times+=1
        check-=1
        
    result=f'執行次數:{times}次'
    return result
complex(int(input('測試')))
```

#### 相信基於上述亂七八糟的程式碼後你已經瞭解如何讓你的程式跑快一點了
#### 當然，如果你很討厭某個人或是你的分數是基於程式碼行數的話你也可以寫個需要循環19.8億次的程式噁心一下他。

# 3. 空間複雜度

## 3.1 空間複雜度又是啥

### 首先，先感謝一下現代科技的進步以及傳奇廚神Jason，基本上空間複雜度這個東西基本上沒什麼人在乎。
### ~~有問題的話絕對是你記憶體插不夠多，16gb不夠就插32gb~~。

### 空間相對於時間來說就特別簡單了，就是你程式執行時會產生多少額外變數，這在身爲時間服雜度大師的你眼裡簡直就是一塊小蛋糕。
#### 問題來了：為什麼是額外變數？
#### 答案也很簡單，因為程式碼（變數、函數⋯⋯）所需要的memory在你按下執行的當下已經決定好了，所以問題就只有你執行中多出來變數了。

### 空間複雜度一樣用 Big O 表示法。

### 3.2 常見的空間複雜度


```python
### Case 1

def complex(n:int):
    total=0
    for i in range(n):
        total += n
        print (id(i))
    return total

complex(10)
```

#### 上述程式中，每次迴圈都會多出一個i，故空間複雜度為Ｏ（1）

### 恭喜，你現在已經是個複雜度磚家了，該去Leetcode上面刷題了。
