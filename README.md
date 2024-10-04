# Daily Record
## Day1 10/3
### 1. 观看了9月30号课程的回放，学会了git的基本使用。
```
git add .  //将更改添加到暂存区
git commit -m "modify structs"  //提交暂存区的更改
git push origin main  //推送到远程仓库
```
### 2. 完成了structs,enums,strings和modules的练习题。学会了struct的初始化以及如何用更新模板一部分值，保持其余的不变。熟悉了&str和String的一些操作，如字符串拼接，去除两端空白字符以及替换指定字符串。
```Rust
let your_order = Order{name: String::from("Hacker in Rust"), count: 1, ..order_template}; // 除了name和count，其余的值全部和order_template一致。

input.trim(); // 去除两端空白字符串，返回&str，不会改变input，返回一个新变量
input.replace("cars", "balloons"); //将cars替换为balloons，返回的是String类型，不会改变input
```
## Day2 10/4
