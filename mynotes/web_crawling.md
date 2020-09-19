# Web\_Crawling

Author: SukiXuu Subject: COMP20008 Time: 2020-09-05, 2020 Semester2

## WebCrawling

### 概念--到底是干啥的

* 通过主网站搜取其他的关联网站的Data, 包括子网站

  ```text
  graph  LR
  A[访问目标网页] --> B[get当前界面中的链接]
  B -->|While Loop Repeat| C[访问链接]
  C -->|回到原来的目标继续搜取| B
  ```

  **针对不同网站格式，采用不同逻辑方法**

* 并排格式

  _相当于只到第一个子网站_

  使用For / While Loop一步到位

  ```text
  graph  TB
  A[总网页] --> B[子网页A]
  A[总网页] --> C[子网页B]
  A[总网页] --> D[子网页C]
  A[总网页] --> E[子网页...]
  ```

* 递进格式

  _A-B-C模式_

  Recursion / While Loop一步到位

  ```text
  graph LR
  A[总网页] --> B[子网页A]
  B --> C[子网页A的子网页A1]
  B --> D[子网页A的子网页A2]
  A --> E[子网页B]
  E --> F[子网页B的子网页B1]
  ```

  **Basic Chalenge**

* 没有总网页的information
* 重复爬取 进入死循环
* 无法访问外网
* 网站有安全防御

  **问题**

* 重复的 Infinity Loop, 导致了Crawling失败

  _哪一个方向进行都可以_

  方法：记录下访问过的页面

  List或者Dictionary

* 哪一个方向进行

  **正则表达式**

  import re

  re.match\(\)

  re.search\(\)

  re.sub\(\)

  re.split\(\)

p = re.compile\(regular expression\) p.match\(\)

