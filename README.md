# Minecraft 資料包筆記
首先我們必須知道，對於一個 entity(實體)) 的資料分成 score 和 nbt。  
這邊我們兩個都會提到。  

## scoreboard
首先必須要先創建記分板，格式如下  
```
scoreboard objectives add [計分項目] [基礎統計]
```

計分項目代表這是甚麼樣的分數，你可以自行定義，例如定義為擊殺次數、遊玩時間等等...。  
基礎統計這個計分項目應該跟者甚麼統計數據一起變動，通常是累加型，例如拉弓次數，範例如下
```
scoreboard objectives add bow minecraft.used:minecraft.bow
```
如果不要有統計數據，則將其設為 dummy，範例如下
```
scoreboard objectives add kill dummy
```
## execute command return value
minecraft 每個指令都有 return value，我們要如何使用這些數值?  
使用 execute  
格式大概是
```
execute [to] run [command]
```
可以將一個分數抓出來，存成 nbt，如下
```
execute store result entity @s damage double 1.1 run scoreboard players get @s crossbow.dmg
```
將該指令格式化
```
execute store result(指定傳送指令結果) (entity @s damage)儲存位置 (double 1.1)倍數 run (players get @s crossbow.dmg)指令結果
```
也可以把 nbt 抓出來，存成 score
```
execute store result(指定傳送指令結果) (score @s crossbow.dmg)儲存位置 run (data get entity @s damage)指令結果
```
> 注意，當有當儲存位置是 nbt 才有倍數，因為分數是整數，但 nbt 千變萬化(可以是浮點數)。  

## scoreboard operation
score 除了綁定統計數據，還可以使用指令直接操作，如下
```
scoreboard players add @s crossbow.dmg 1
scoreboard players set @s crossbow.dmg 1
```
scoreboard 後面接 players，代表我們要直接對 entity 的某項分數進行操作，