# 游戏策划
## 大背景：一个无名人类英雄不小心闯入怪物的世界，这个世界里的怪物可以瞬间出现在任何位置。怪物们从未见过人类，因此非常渴望捕杀英雄，英雄从此踏上求生之路。

## Player：无名英雄，怪物
## Boss：九头怪
## 器物：武器，子弹
## 特效：怪物死亡时的爆炸特效，子弹弹道，子弹打在怪物上的爆炸特效

# 游戏设计

## | 无名英雄   |
## | Every tick | 
## | Set angle toward(Mouse.X,Mouse.y) |

## | On Left button Clicked |
## | Spawn 子弹 Bullet On 怪物 |

## | 怪物   |
## | On collision with 怪物 | 
## | Spawn 爆炸特效 on 怪物|

## | On start of layout | 
## | Set angle to 360 degress |

## | is outside layout | 
## | Set angle toward(无名英雄.X,无名英雄.y) |