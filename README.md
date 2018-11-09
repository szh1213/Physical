# 物理运动

通过代码实现物理运动，实现物理数字化

匀速直线运动（牛顿第一定律）

```java
float x;
void setup()
{
  size(666,233);
}

void draw()
{
  background(158);
  rect(x++,height/2,23,23);
}
```
