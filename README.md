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
### 完成了hashmap练习题,在对hashmap进行修改时，不能同时取出一个以上的mut变量修改。
```Rust
let mut& basket: HashMap<Fruit, u32>;
baskey.entry(fruit).or_insert(100); //如果不存在fruit，则插入并赋值为100
```
## Day3 10/5
### 完成了options,error_handling,generics,quiz2,traits练习题。
```Rust
//在match语句中使用条件语句进行判断
match time_of_day {
    x if x < 22 => Some(5),
    x if x < 24 => Some(0),
    _ => None,
}

//将Option转为Result类型使用map_or，into函数对于实现了Into特征的类都可以进行类型转换
assert_eq!(
    generate_nametag_text("Beyoncé".into()).map_or(Err("`name` was empty; it must be nonempty."), |v| Ok(v)),
    Ok("Hi! My name is Beyoncé".into())
);

//?可以提取Option和Result中Some()和Ok()中的值，如果是None或Err则会返回None或Err
let qty = item_quantity.parse::<i32>()?;

//Vec的pop方法返回的是Option类型
while let Some(Some(integer)) = optional_integers.pop() {
    assert_eq!(integer,cursor);
    cursor -= 1;
}

//Box<dyn Trait> 可以动态分配，实现多态
```

