# L03 Data Formats

Overview Data Formats Unstructured Semi-structured Structured Pre-processing Why? How?

Part-01 Data Formats Outline Questions: What data formats might I encounter? &lt;我可能会遇到哪些数据格式?&gt; Why do we have different data formats? &lt;为什么我们有不同的数据格式&gt; Why do we want to transform between different formats? &lt;为什么我们要在不同的格式之间转换&gt;

[avator](https://github.com/SukiXuu/websetting/tree/0aadb01b81fe627c447b9ad1e936219cc6e1a8cd/courses/COMP20008/mynotes/mynotes/截屏2020-08-21%20上午2.08.09.png) Examples of Data Formats Unstructured Semi-Structured Structured Text files/documents XML Databases Audio JSON Tables Video Webpages Spreadsheets Social media data  
五花八门, 各式各样 标题, 内容 表格式的 More Machine Readable More Human Readable

Relational Database 并不意味着不需要设计; 相反, 这些数据/table之间的关系是很重要的 Advantge of a well designed database: Linking the relevent infomations from other table 而不是repeating info \(Main\) Normalzation: In this case means 把一些表格的信息总合在一个表格里

```text
DBMS - Database Management System
    Persistent in nature  可用的时间长
SQL - a langurage used for relational databases
    Create table
        branch 
        branch_name    Char(15) not null,
        branch_city    char(30)
        assets    integer
        primary    key (branch_name)
    select account.balance 
    from depositor, account (join syntax which throw "where")
    where depositor.customer_id = ‘192-83-7465’ and 
        depositor.account_number = account.account_number

与INFO20003相关的Topic: 
    SQL
    Specification of integrity constraints
    Data modelling and relational database management systems
    Transactions and concurrency control
    Storage management
    Web-based databases

Relational Algebra 
    import pandas as pd 
    pd.merge()
        on/how/inner/outer/left/right 
    Compare:
        concat/append
```

Part-02 -- DataFrame in Pandas 合并

Key / Keys \(find the subset to merge the DataFrames\) 1. Inner join: 两个DataFrames都有的部分 pd.merge\(A, B, on=\[' '\]\) // 会自动加重复的key 2. Outer join: Left join: 左边的enery加右边的data Right join: 右边的entries加左边的data pd.merge\(A, B, key="outer"\) pd.merge\(A, B, key="left"\) pd.merge\(A, B, key="right"\) pd.merge\(A, B, left\_on=\[""\], right\_on\[""\]\) //当A和B的key的名字不一样的时候

Panda-Resources: [https://jakevdp.github.io/PythonDataScienceHandbook/03.07-merge-and-join.html](https://jakevdp.github.io/PythonDataScienceHandbook/03.07-merge-and-join.html) [https://jakevdp.github.io/PythonDataScienceHandbook/03.06-concat-and-append.html](https://jakevdp.github.io/PythonDataScienceHandbook/03.06-concat-and-append.html) [https://pandas.pydata.org/pandas-docs/version/0.22.0/merging.html](https://pandas.pydata.org/pandas-docs/version/0.22.0/merging.html)

Challenges Once data is into a relational database, it is easier to wrangle. But may be difficult to load it there in the first place ???

More structure - Spreadsheets Huge amounts of data is in spreadsheets Businesses Hospitals …

```text
Microsoft (Excel), OpenOffice (Calc), Google docs
Tabular
```

Part-03 -- Semi-structured

1. CSV: comma separated values Also very popular Also stores tabular information Lacks formatting information Does not contain formulas and macros for data verification, transformation Just a delimited text file with extension .csv human readable, versus binary XLS format \(Excel\) manipulate with any text editor Example – CSV Ingest into spreadsheets Easy to use Structured, but not like excel or a relational DB
2. HTML – Hypertext Markup language Marked up with elements -- delineated by start and end tags There are a few exceptions, so not _all_ elements need both start and end tags Elements correspond to logical units, eg. heading, paragraph or itemised list can have attributes; ordering of attributes is not significant Tags: Keywords contained in pairs of angle brackets. Not case sensitive Browser determines how to display/present the logical units HTML Example

Limitations of HTML --- 不统一 HTML was designed for pure presentation HTML is concerned with formatting not meaning it doesn’t matter what it is about, HTML will format it HTML is not extensible can’t be modified to meet specific domain knowledge browsers have developed their own tags \(, \) HTML can be inconsistently applied almost everything is rendered somehow e.g. is this acceptable? &lt;/&gt;

1. XML: eXtensible Markup Language Extensible: user defined tags A ‘meta’ mark-up language Facilitate better encoding of semantics Example: Subject Guide Year of offer = 2019 Subject level = Undergraduate level 2 Subject code = COMP20008 Campus = Parkville Availability = Semester 1, Semester 2

   相对而言XML易于修改

XML syntax – well formed xml files must begin with declaration &lt;?xml version="1.0"?&gt; xml elements • One root element Appropriately nested Start/end tags or Empty tags Attributes in quotes  Parkville &lt;/campus&gt; or  Case sensitive Comments  Some characters have special meaning e.g: '&lt;', '&' 就要用 '&', '⁢' CDATA\(character data\) Section may be used inside XML element to include large blocks of text, which may contain these special characters such as &, &gt;. 大量文本的输入, 就有可能运用到这些字符转换 Using HTML/XML \(Python\) 数据包的运用 For HTML scraping, the Beautiful Soup library is good For XML, a good library is [http://lxml.de/](http://lxml.de/) Import the XML file into your program as a tree structure: import xml.etree.ElementTree as ET tree = ET.parse\(‘yourfile.xml'\) root = tree.getroot\(\) Then loop through root with the various methods available: for child in root: print child.tag, child.attrib

[原本onenotes版本](https://unimelbcloud-my.sharepoint.com/personal/jixu5_student_unimelb_edu_au/_layouts/OneNote.aspx?id=%2Fpersonal%2Fjixu5_student_unimelb_edu_au%2FDocuments%2F%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86&wd=target%28%E6%96%B0%E5%88%86%E5%8C%BA%201.one%7CD9E45E07-62DE-8345-8E02-563EEAD70796%2FLecture%203%20--%20Data%20Format%7C5040D2E0-F6CB-D144-8C24-5D97CFCCB534%2F%29%20onenote:https://unimelbcloud-my.sharepoint.com/personal/jixu5_student_unimelb_edu_au/Documents/数据处理/新分区%201.one#Lecture%203%20--%20Data%20Format&section-id={D9E45E07-62DE-8345-8E02-563EEAD70796}&page-id={5040D2E0-F6CB-D144-8C24-5D97CFCCB534}&end)

